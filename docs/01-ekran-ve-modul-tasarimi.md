# Ekran ve Modül Tasarımı (V9)

## Ürün ilkeleri
- **Telefon ana cihazdır:** personel ve yönetici günlük tüm işlemleri mobilde yapar.
- **PC yalnızca toplantı içindir:** gündem, istişare, karar, görev çıkarımı ve gündem PDF.
- Girişler kısa ve tek amaçlıdır. Personel bir seferde **tek konu** yazar; kişi, tarih, durum otomatik gelir.
- Görsel tema: başlık #092F62; açık mavi #C9E8FF; sorun pembe #F8D5E1; talep mint #C8EFD9; görev turuncu #FFE2AD; açık zemin #EFF8FF.
- Kartların köşeleri yumuşak, alt gezinme sabit, 44px ve üzeri dokunma alanları. Hareket azaltma ve ekran okuyucu desteği.
- Gizli/özel konular ortak gündemde herkese açık **gösterilmez**. Yönetici güvenlik kontrollerini uygular.

## 1. Personel ekranı – mobil ana sayfa
**Kartlar:** Toplantı Gündemi / Sorun Bildir / İhtiyaç-Talep / İşlerim.
- Üstte ad, rol, okunmamış görev uyarısı.
- Sorun formu: tek satır "Sorun nedir?", opsiyonel açıklama/fotoğraf, "Acil" tek işaret.
- Talep formu: tek satır "İhtiyaç nedir?", opsiyonel detay.
- Kaydedilince konu kodu ve durumu gösterilir; internet hatasında çift gönderme engellenir.
- Alt gezinme: Ana Sayfa, Gündem, İşlerim; yönetici için Yönetim.

## 2. Ortak toplantı gündemi
- Onaylanmış ve bekleyen *genel* gündem başlıkları tek listede; arama en üstte.
- Madde: başlık, kategori, durum, destek sayısı, "Ben de katılıyorum"; her kullanıcı en fazla bir kez destekler.
- Yeni başlık için yalnız başlık gerekir. Gönderilmeden önce benzer maddeler gösterilir.
- Yönetici onaylar, birleştirir veya hassas maddeyi özel alanda tutar. Birleştirmede eski kayıt bağlanır; geçmiş kaybolmaz.
- Onaylı maddeler otomatik PDF toplantı gündemine girer.

## 3. Yönetici mobil paneli
- 4 KPI: Yeni bildirim, onaylı gündem, açık görev, takip gerektiren.
- İşlem listesi: acil önce, sonra gecikme, destek bekleyen, yeni; tamamlananlar arşivde.
- Bildirim satırında görev ata / toplantıya al / gerekçeyle kapat veya birleştir.
- Personel yönetimi: aktif personel, rol, çalışma alanı, bağlantı paylaşımı; e-posta daveti **sunucu tarafı güvenli davet hizmeti** olmadan otomatik gönderilmez.

## 4. Yönlendirme / görev verme
- Sorun veya talepten açılır, kaynak kaydı kaybolmaz.
- Atama: sorumlu, son tarih, öncelik; açıklama opsiyonel.
- Acil = anında ilk müdahale; istişare de gerekiyorsa **aynı kayda bağlı ikinci gündem**.
- Personel görevi kendi telefonunda görür; tamamlandı veya destek gerekiyor diyebilir.
- Yönetici doğrulama gereken görevlerde kapamayı onaylar.
- Kaynak bildirim ve görev referansları üzerinden izlenebilir geçmiş tutulur.

## 5. Toplantı yönetimi – PC / projeksiyon
- Tarih-saat/yer, toplantıyı başlat/bitir, solda gündem, ortada görüşme/istişare, sağda karar.
- Madde seç: geçen haftanın açık kararları görünür; istişare notunu yaz, sonra karar ekle.
- Karar: tek metin, opsiyonel birden çok alt görev, her görev için sorumlu ve takip tarihi.
- İşlemler: Kaydet, Sonraki Madde, Görüşüldü olarak işaretle; toplantı sonunda sonuçları onayla.
- Kararlar toplantı kapanmadan kaydedilir; aynı bilginin tekrar girişi olmaz.

## 6. Toplantı özeti ve kararlar
- Toplantı başlığı, zaman, katılımcılar (opsiyonel), görüşülen madde sayısı, kısa özet.
- Karar tablosu: karar, kaynak gündem, sorumlu, son tarih, görev durumu.
- Personel kendisine duyurulan genel kararları okur; sadece yönetici düzenler.
- Toplantı karar özeti PDF / paylaşım dosyası olabilir.

## 7. Geçen haftanın icra durumu
- Önceki toplantının kararlarından doğan görevleri filtrele.
- İcra oranı: **doğrulanmış veya tamamlanmış görev / takip edilecek toplam görev**; payda ve tarih aralığı açık yazılır.
- Sayılar: tamamlandı, sürüyor, engelli, gecikti. Gecikme = son tarih geçmiş + tamamlanmamış.
- Yeni toplantının ilk sayfasında en fazla 5 öncelikli gecikmiş kayıt göster.
- KPI değerleri kayıtlarla hesaplanır, tasarımdaki örnek sayılar kullanılmaz.

## 8. Gündem maddeleri PDF
- A4 portre, tarih, saat, yer, numaralı başlıklar, altına **en az 3 not satırı**.
- Yalnızca yönetici tarafından onaylanan, toplantı kapsamındaki genel maddeler.
- Yazdır / PDF olarak kaydet (telefonla indirilebilir; esas kullanım PC).
- Gizli kişisel bilgiler, telefon numaraları ve kapalı bildirimler çıktıya alınmaz.

## Kabul kriterleri
1. Personel yeni sorun/istek için zorunlu en çok 1 metin alanı doldurur.
2. Bir kullanıcı aynı gündeme iki kez katılamaz.
3. İstişare gerekmeyen işler toplantıyı beklemez.
4. Yönetici yalnızca yetkili olduğu personeli görevlendirir.
5. Bir karar 0..N göreve bağlanabilir; görev sonucu kaydın geçmişinde görünür.
6. Toplantı ekranı projektörde okunabilir; PDF A4 baskıda taşmaz.
7. Yetkisiz kullanıcının görev ataması/veri okuması veritabanında engellenir.
8. Gerçek kişi verisi hiçbir demo/test çıktısına kopyalanmaz.
