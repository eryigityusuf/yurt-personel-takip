# Mobil menü, sayfa akışı ve bilgisayar görünümü

## Mobil navigasyon (tek elle kullanım)
**Alt çubuk:** Ana Sayfa | Gündem | İşlerim | Yönetim (yalnız yönetici).
**Ana ekran hızlı işlem kartları:** Gündem, Sorun Bildir, İhtiyaç/Talep, İşlerim.

```mermaid
flowchart TD
 A[Telefon: Ana Sayfa] --> B[Gündem]
 A --> C[Sorun Bildir]
 A --> D[İhtiyaç Talep]
 A --> E[İşlerim]
 B --> F{Benzer konu var mı?}
 F -->|Var| G[Ben de katılıyorum]
 F -->|Yok| H[Tek satır öneri]
 C --> I[Yönetici kuyruğu]
 D --> I
 H --> J[Onay kuyruğu]
 J --> K[Toplantı gündemi]
 I --> L{Yönlendirme}
 L -->|Görev| E
 L -->|İstişare| K
 K --> M[PC Toplantı Salonu]
 M --> N[Karar]
 N --> O[Atanmış Görevler]
 O --> E
 ```

## Personel akışları
- Gündem: liste → arama → katıl veya yeni öneri → kayıt sonucu.
- Sorun: tek satır → acil işareti (opsiyonel) → gönder → bildirdiklerim.
- Talep: tek satır → gönder → durum takibi.
- İşlerim: görev detayı → tamamladım / destek gerekiyor → not (opsiyonel).

## Yönetici telefonda
- Yönetim: işlem bekleyenler → Bildirim detay → sorumlu/son tarih → görev ata veya gündeme ekle.
- Personel yönetimi: personel listesi → görevlendir; yeni personel için kayıt bağlantısı paylaş.
- Gündem: önerileri sırala / birleştir / onayla.
- Takip: engelli/gecikmiş görevleri öne çıkar, çözüme karar ver.

## Toplantı salonu bilgisayarı
- 16:9 geniş ekran, solda onaylı gündem, ortada seçili madde ve istişare, sağda karar formu.
- Üst: tarih, saat, konum, oturum durumu.
- Alt: Geçen haftanın icrası ve bir sonraki madde düğmesi.
- Karar kaydet → görev listesine bağla; toplantı bitir → özet / PDF.
- Projektörde isim/kişisel hassas bildirimlerin görünmesini önle.

## Erişilebilirlik ve çevrimdışı davranış
- Her buton 44px ve üzeri dokunma hedefi; odak çerçevesi ve aria etiketi.
- Renk tek başına durum belirlemez: etiket ve ikon da görünür.
- İnternet yokken yeni kayıt **gönderildi denilmez**; bağlantı geri gelince yeniden gönderme önerilir, çift kayıt önlenir.
- PWA ana ekrana eklenebilir; güvenilir çevrimdışı yazma ayrıca tasarlanmalıdır.
