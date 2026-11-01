# Supabase veri modeli ve güvenlik tasarımı

**Mevcut proje:** `zuqrjysgejsqpdthzrbx`. Canlı veriler korunacak; değişiklikler ayrı versiyonlu migration olarak uygulanacak. Mevcut yedi tablo silinmeyecek.

## Mevcut tablolar (uygulanmış)
| Tablo | Amaç | Önemli bağlar |
|---|---|---|
| profiles | Personel adı ve rol | id = auth.users.id |
| agenda_items | Gündem önerileri ve onay durumu | created_by |
| agenda_supports | Tekil "katılıyorum" | (agenda_id,user_id) birleşik anahtar |
| reports | sorun / ihtiyaç / talep | created_by, urgency, status |
| meetings | toplantı başlıkları ve zamanları | created_by |
| decisions | toplantı kararları | meeting_id, agenda_id |
| tasks | iş ve görevlendirme | report_id, decision_id, assigned_to |

Bu yedi tabloda RLS etkin. Varsayılan kayıt rolü staff; yönetici rolü **yalnızca idari kanaldan** atanır. Public anon/service anahtarı veya veritabanı şifresi istemciye koyulmaz.

## Planlanan ek yapılar (henüz uygulanmadı)
| Tablo / alan | Amaç | Kural |
|---|---|---|
| meeting_agenda (meeting_id, agenda_id, ordering) | Gündemi belirli toplantıya bağlama | birleşik benzersiz anahtar, manager yazma |
| meeting_notes (meeting_id,agenda_id,note,author_id) | İstişare notu | manager yazma; gizlilik sınıflaması |
| task_events (task_id,actor_id,old_status,new_status,note,at) | Denetlenebilir işlem geçmişi | append-only; kullanıcı kendi olayını ekler |
| report_attachments (report_id,storage_path,uploaded_by) | Fotoğraf referansı | private Storage bucket ve erişim denetimi |
| reports.visibility | general / restricted | yalnız genel kayıtların ortak paylaşımı |
| agenda_items.visibility | general / restricted | kısıtlı gündemi herkese açık SELECT'ten çıkar |
| agenda_items.merged_into | tekrar kaydı özgün kayda bağlama | aynı kayıt geçmişini koru |
| tasks.requires_verification | müdür onayı gerektiriyor mu? | manager ayarlar |
| tasks.completed_at,verified_at | hesaplanabilir tamamlanma | zaman damgası |
| profiles.active,department | personel seçimi ve arşiv | rol güncellemesi yalnız yönetici |
| decision task links | Bir kararın çok görevi zaten tasks.decision_id ile mümkündür | FK korunur |

## Erişim matrisi
| Veri | Personel | Yönetici |
|---|---|---|
| Kendi profil bilgisi | oku | tüm personeli oku |
| Genel onaylı gündem | oku/katıl | oku/katıl/onayla |
| Yeni genel gündem önerisi | oluştur | oluştur/onayla/birleştir |
| Kendi sorun-talep kaydı | oluştur/oku | tümünü değerlendir |
| Gizli sorun-talep | yalnız oluşturana göster | yetkili yönetici |
| Kendi görevi | oku; yalnız durum/sonuç güncelle | ata, düzenle, doğrula |
| Toplantı/karar | duyurulmuş genel veriyi oku | oluştur/güncelle |
| Denetim kaydı | kendisiyle ilgili | yönetici raporları |

## Kritik güvenlik işleri
- **Şimdiki task UPDATE** politikası yalnız yöneticiye izin veriyor. Personelin tamamlandı/destek gerekiyor işlemi için ayrı **sınırlandırılmış RPC veya tetikleyici + RLS** gerekir. Mevcut yetkiyi gelişi güzel genişletme.
- **Şimdiki agenda_items SELECT** tüm oturumlu kullanıcılara açıktır. Kısıtlı gündem eklemeden önce görünürlük politikasını güncelle.
- **Şimdiki profiles SELECT** tüm oturumlu kullanıcılara açıktır. Uygulama yalnızca gerekli alanları gösterse bile RLS ve veri erişimi ihtiyaca göre kısıtlanmalı.
- OAuth/email doğrulama redirect URL, Supabase Auth site URL ve Github Pages adresi eşleşmeli.
- Görev atamada isim yerine kimlik (UUID) kullanılmalı; anonim oturum kapalı tutulmalı.
- Storage özel bucket, uzantı/boyut sınırı, dosya sahipliği ve silme politikası olmalı.
- Yönetici rolünü kullanıcının düzenleyebildiği metadata'ya bağlama.
- Tüm schema migration'ları staging ortamında sınanmalı, backup ve rollback notu tutulmalı.

## İlişkiler
`auth.users 1—1 profiles`
`auth.users 1—N reports / agenda_items / tasks(assigned_to)`
`agenda_items N—N auth.users (agenda_supports)`
`meetings N—N agenda_items (meeting_agenda)`
`meetings 1—N decisions`
`decisions 1—N tasks`
`reports 1—N tasks`

## Yayın kontrolü
RLS advisors → erişim politikaları → personel/yönetici hesap testi → veri erişim regresyonu → sonra migration üretimi. Gerçek veritabanı değişikliğini bu belge oluşturmaz.
