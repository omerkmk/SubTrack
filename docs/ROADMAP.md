# SubTrack Yol Haritası

## Vizyon
Türkiye odaklı abonelik ve fatura takipçisi. Dolar ve euro bazlı abonelikleri güncel kurla
TL'ye çevirir; yenilemeden ve ücretsiz deneme bitmeden önce hatırlatır.

`SubTrack` kod adıdır; App Store adı ayrı olacak. Yayından önce: App Store araması ve
TÜRKPATENT / EUIPO / USPTO marka kontrolü.

## Teknik kararlar
- UIKit, programatik UI. Tek istisna: Faz 3'teki widget SwiftUI (WidgetKit sadece SwiftUI).
- Mimari: MVVM-C. VIPER ve Clean Swift learning-lab'da çalışılır, projeye girmez.
- Para için `Double` değil `Decimal`.
- Firebase Faz 2'de. MVP'de veriler sadece telefonda; depolama yöntemi
  (Core Data / SwiftData / dosya) bir sprintte bilerek seçilecek.
- Modülerlik SPM yerel paketleriyle; Tuist yok.
- Sadece iPhone, sadece dikey (portrait), minimum iOS 17.0.

## Döviz kuru API'si: Frankfurter
[frankfurter.dev](https://frankfurter.dev), 17 Kasım 2026'da doğrulandı.
- TRY destekli. Anahtar yok, ticari kullanım serbest, kota yok; önbelleğe almayı öneriyorlar.
- Referans kur, anlık değil → uygulamada "yaklaşık" yazılır.
- Servis bir protokolün arkasında durur; gerekirse başka API'ye geçilebilir.
- `api.frankfurter.app` → `api.frankfurter.dev`'e yönleniyor; v1 eski, v2 güncel.
- Elenen: ExchangeRate-API (zorunlu atıf + otomatik kullanım için belirsiz madde).

## Faz 1: MVP (TestFlight)
1. Abonelik ekle / düzenle / sil: ad, tutar, para birimi (₺ / $ / €), periyot,
   sonraki yenileme, kategori
2. Hazır şablonlar: Netflix, Spotify, YouTube Premium, iCloud+, ChatGPT Plus, Disney+,
   Exxen, Amazon Prime… (fiyat düzenlenebilir, "tahmini")
3. Özet ekranı: bu ay toplam ₺, yıllık tahmin, önümüzdeki 7 günün yenilemeleri
4. Kur dönüşümü: $ ve € → ₺, "yaklaşık" + son güncelleme; offline'da son kur
5. Yenileme hatırlatması: 1 / 3 / 7 gün önce bildirim
6. Deneme süresi uyarısı ("Deneme yarın bitiyor, iptal etmezsen ₺149 çekilecek")
7. Onboarding: 2-3 sayfa + bildirim izni (bilerek storyboard ile)

Ekranlar: Onboarding · Özet · Liste · Ekle/Düzenle · Detay · Ayarlar

## Faz 2: Bulut ve kalite
- Firebase: Sign in with Apple, Firestore senkron, uygulama içi hesap silme,
  gizlilik politikası ve etiketleri
- Kategori halka grafiği
- Kur etkisi ("Kur yüzünden bu ay ₺85 fazla")
- Deep link (bildirim → detay)
- TR / EN
- Arama, filtre, sıralama
- SPM paketleri, XCConfig, UI ve snapshot test, Fastlane

## Faz 3: İleri seviye
- Widget
- Paylaşılan abonelik (aile planında kişi başı)
- Animasyon ve özel geçişler
- CSV dışa aktarma
- Instruments ile performans

## Bilerek olmayacaklar
- Banka / kart bağlantısı
- Uygulamadan abonelik iptali
- Anlık kur, yatırım
- Reklam ve uygulama içi satın alma

## App Store hazırlığı
- Apple Developer Program üyeliği (yıllık ücretli) TestFlight öncesi gerekir.
- Demo ya da klon görünmemeli (Guideline 4.2 / 4.3): fark Türkiye odağı.
- Hesap varsa: uygulama içi hesap silme, gizlilik politikası, gizlilik etiketleri,
  Sign in with Apple.
- İkon: 1024×1024, saydamlıksız PNG.
