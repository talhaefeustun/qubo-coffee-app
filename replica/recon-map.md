# Qubo Coffee App — Recon Map

Yöntem: `replica-recon` skill'inin adımları (kapsam → kaynaklar → ekran envanteri → akışlar → bileşenler → veri modeli → özellik matrisi → kapsam dışı → boyutlandırma).

## 1. Kapsam
- Ürün: Qubo Coffee franchise zinciri için müşteri tarafı kafe uygulaması (mobil öncelikli web uygulaması, her şubede kullanılabilir).
- Çekirdek döngü: Şube seç → Menüden ürün seç ve özelleştir → Sepet → Gel-al siparişi ver → Sipariş durumunu izle → Qubo Club puanı kazan.
- Referans alınan kafe uygulamaları (genel özellik kalıpları): Starbucks TR, Kahve Dünyası, Espressolab, Coffy, Kocatepe Kahve. Sadece akış ve ekran kalıpları alındı; içerik, görsel ve metin alınmadı.

## 2. Kaynaklar
| Kaynak | URL |
|---|---|
| Qubo Coffee ana sayfa | https://www.qubocoffee.com/ |
| Menü (8 kategori, 186 ürün) | https://www.qubocoffee.com/menu |
| Şubeler (10 şube) | https://www.qubocoffee.com/subelerimiz |
| Hakkımızda | https://www.qubocoffee.com/hakkimizda |
| Replica skill | https://github.com/Jakeschincariol/replica-skill |

## 3. Ekran envanteri
| ID | Ekran | Rota | Amaç | Bileşenler | Durumlar |
|---|---|---|---|---|---|
| S01 | Ana sayfa | #home | Karşılama, şube, Qubo Club kartı, kampanyalar, popüler ürünler | Header, BranchChip, LoyaltyCard, PromoCarousel, ProductRow, CategoryGrid | dolu, şube seçilmemiş |
| S02 | Menü | #menu | Kategori + arama ile ürün keşfi | SearchBar, CategoryChips, ProductCard grid | dolu, arama boş sonucu |
| S03 | Ürün detayı (sheet) | modal | Boy / süt / şurup / ekstra shot / adet seçimi | OptionGroup, Stepper, PriceBar, AddButton | varsayılan, seçili |
| S04 | Sepet | #cart | Ürünleri düzenle, teslim şubesi ve saati, özet | CartLine, Stepper, BranchPicker, TimePicker, Summary, CTA | boş, dolu |
| S05 | Sipariş durumu | #order | Sipariş alındı → hazırlanıyor → hazır | ProgressSteps, OrderCode, OrderLines | alındı, hazırlanıyor, hazır |
| S06 | Şubeler | #stores | Şube listesi, açık/kapalı, seç, ara, yol tarifi | StoreCard, StatusPill, ActionButtons | dolu |
| S07 | Qubo Club / Hesabım | #club | QR kart, puan, damga, geçmiş, ayarlar | QRCard, StampRow, HistoryList, SettingsList | yeni üye, puanlı |
| S08 | Kampanyalar | #promos | Aktif kampanyalar | PromoCard | dolu |

## 4. Kullanıcı akışları
1. **Gel-al sipariş (çekirdek):** S01 → S02 → S03 → S04 → S05. Mutlu yol tık sayısı: 6.
2. **Şube değiştir:** S01 (chip) → S06 → Seç → S01.
3. **Puan kullan:** S07 → QR göster (kasada okutma) → damga/puan güncellenir.
4. **Tekrar sipariş:** S07 geçmiş → "Tekrar sipariş ver" → S04.

## 5. Bileşenler
Header, BottomTabBar(5 sekme), BranchChip, LoyaltyCard, PromoCarousel, CategoryChip, ProductCard (grid/row varyantları), OptionGroup (tek seçim), Stepper, Sheet (alt panel), Toast, StatusPill, ProgressSteps, QRCard, EmptyState.

## 6. Veri modeli (çıkarım)
- Branch(id, city, district, address, hours, image, phone, lat/lng?) — güven: yüksek (site)
- Category(id, name) — yüksek
- Product(id, categoryId, name, image, basePrice, sizes?, options?) — fiyatlar sitede yok → örnek fiyat
- CartItem(productId, size, milk, syrup, extraShot, qty, note)
- Order(code, branchId, items, total, status, createdAt, pickupTime)
- Member(name, points, stamps, tier, history[])

## 7. Kapsam dışı
- Gerçek ödeme (skip: PSP entegrasyonu gerekir; demo "Kasada öde / Kayıtlı kart" seçimi var)
- Harita gömme (skip: artifact ortamı iframe izin vermiyor; Google Maps linki var)
- Push bildirim (skip: web demo)

## 8. Boyutlandırma
8 ekran, 4 akış, 6 varlık. Zor kısımlar: ürün özelleştirme (M), çoklu şube durumu (S), sipariş durum simülasyonu (S). Toplam: M.
