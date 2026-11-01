# Yurt Personeli Toplantı ve Görev Takip Sistemi

Mobil öncelikli web uygulaması. Supabase projesi: `zuqrjysgejsqpdthzrbx`.

## Durum
Supabase'de 7 tablo ve RLS politikaları oluşturuldu. Bu depo uygulama istemcisini barındırır. Personel hesapları ve yönetici rol atamaları tamamlanmadan gerçek kullanım başlamamalıdır.

## Yayınlama
GitHub Pages: Settings > Pages > Deploy from a branch > main / root. Alan adı aktif olunca Supabase Auth URL Configuration içindeki Site URL ve Redirect URLs güncellenmelidir.

## Güvenlik
`service_role` ve veritabanı parolası asla repoya eklenmemelidir. Gizli personel verileri GitHub'da saklanmaz.
