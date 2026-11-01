# Kullanıcı senaryoları ve uçtan uca test planı

## Personel senaryoları
**P1 — Yeni genel gündem:** Personel 'Temizlik saatlerinin düzenlenmesi' girer → öneri durumu → yönetici onayı → ortak listede görünür.

**P2 — Tekrar kayıt önleme:** Başka personel benzer gündemi arar → mevcut kayda 'Ben de katılıyorum' → yeni başlık yok; ikinci katılım benzersizlik nedeniyle reddedilir.

**P3 — Acil sorun:** Personel 'Su kaçağı' bildirir ve Acil seçer → yöneticinin kuyruğunda acil işaretli → mevcut acil müdahale kanalından da haber verir → yönetici hızlı görev atar → kalıcı çözüm gerekirse gündeme ekler.

**P4 — İhtiyaç:** 'Temizlik malzemesi eksik' → personel gönderir → yönetici mevcut rutin iş olarak görevlendirir → personel ilerlemeyi takip eder.

**P5 — Görev tamamlama:** Kendine atanan görevi açar → 'Tamamladım' der → kontrol gerekiyorsa yönetici doğrulama kuyruğuna düşer. Şu anki RLS bu personel güncellemesini henüz desteklemiyor; uçtan uca test bekliyor.

**P6 — Destek gerekiyor:** Görevde engel oluşur → 'Destek gerekiyor' ve opsiyonel not → yönetici engeli görür, sonraki adımı belirler.

## Yönetici senaryoları
**Y1 — Onay:** Genel gündemi onaylar → status approved; PDF listesinde yer alır.

**Y2 — Doğrudan atama:** Bildirim seçer → listeden sorumlu ve son tarih → görev açılır, kaynak bildirim assigned olur.

**Y3 — Toplantıya yönlendir:** İstişare gerektiren bildirim tek kayıt üzerinden gündeme bağlanır; mükerrer bildirim oluşmaz.

**Y4 — Toplantı kararı:** PC'de toplantıyı başlatır, gündem seçer, not ve karar kaydeder → karar için 1-3 görev atar → görevler personellerin telefonunda görünür. Bu tam akış henüz kodda uygulanmadı.

**Y5 — Kapanış:** Tamamlanan görevleri doğrular ve haftalık icra raporunu inceler.

## Kontrol listesi
- [x] Supabase Auth hesap açma ve oturum açma (canlı kullanıcı testi)
- [x] Personel gündem maddesi oluşturma (canlı kullanıcı testi)
- [x] Yönetici rolü atama (veritabanında doğrulandı)
- [x] Yönetici gündem onayı (veritabanında doğrulandı)
- [x] Acil sorun bildirimi oluşturma (veritabanında doğrulandı)
- [ ] İkinci personel hesabı / davet
- [ ] Gerçek personel görevi görme ve güncelleme
- [ ] Rol/RLS olumsuz testleri (yetkisiz görev atama, rol değiştirme, kapalı gündem)
- [ ] PC toplantı ve karar akışı
- [ ] Bir karardan çoklu görev
- [ ] Geçen hafta icra hesaplaması
- [ ] PDF A4 baskı testi
- [ ] Mobil Safari ve Android Chrome ekran testi
- [ ] PWA install ve çevrimdışı durum mesajı
- [ ] Temizlik / veri tutarlılığı / geri yükleme denemesi

## Gerçek kullanıma geçiş eşiği
Çok kullanıcılı test, yetki güvenliği, görevlerin personelce tamamlanması, toplantı-karar-görev zinciri ve çıktı doğrulanmadan 'üretime hazır' statüsü verilmez.
