# Qubo Coffee App

Qubo Coffee franchise şubeleri için mobil öncelikli kafe uygulaması (tek dosya, bağımlılık yok).

## Çalıştırma
- `index.html` dosyasını doğrudan tarayıcıda açın, veya
- Bir statik sunucu ile: `npx serve .` (ya da `.claude/launch.json` içindeki `qubo-app` yapılandırması).

## Ekranlar
Anasayfa · Menü (8 kategori, 160 ürün) · Ürün özelleştirme (boy / süt / şurup / ekstra shot) · Sepet ve gel-al · Sipariş durumu · Şubeler (10 şube) · Qubo Club (puan, damga, QR, geçmiş)

## Yapı
- `index.html` — uygulama (CSS + JS tek dosyada). Ürünler `CATS`, şubeler `STORES`, kampanyalar `PROMOS` dizilerinde.
- `assets/` — qubocoffee.com'dan alınıp küçültülmüş görseller (webp).
- `replica/` — replica-skill yöntemiyle hazırlanan keşif haritası, tasarım token'ları ve özellik matrisi.

## Notlar
- Fiyatlar örnektir; her ürün `CATS` içinde `base` aralığından türetilir. Gerçek fiyatlar için `PRODUCTS` üretimini düzenleyin.
- Sepet, seçili şube ve üye bilgisi tarayıcının localStorage'ında tutulur. Gerçek kullanım için bir backend (ör. Supabase) bağlanmalıdır.
- Ödeme ve harita gömme kapsam dışıdır (bkz. `replica/features.csv`).
