# Phase Loop

Tek dosyalı HTML5 mobil oyun (Canvas + Vanilla JS). Android'e paketlemek için Capacitor tabanlı kurulum dosyaları repo içinde hazırlandı.

## İçerik

- `index.html`: Oyunun tüm kodu (UI, oyun döngüsü, ses, titreşim, reklam simülasyonu, localStorage).
- `package.json`: Gerekli npm bağımlılıkları ve komutlar.
- `capacitor.config.ts`: Android uygulama kimliği ve proje ayarları.

## Android AAB Alma (Adım Adım)

> Gereksinimler: Node.js 18+, Android Studio (SDK + Build Tools), Java 17.

1. Bağımlılıkları kur:

```bash
npm install
```

2. Android platformunu oluştur (ilk kurulumda):

```bash
npx cap add android
```

3. Web dosyalarını Android projesine senkronla:

```bash
npx cap sync android
```

4. Android Studio ile aç:

```bash
npx cap open android
```

5. Android Studio içinde:
   - `Build > Generate Signed Bundle / APK`
   - `Android App Bundle` seç
   - Yeni keystore oluştur veya mevcut keystore seç
   - `release` varyantı ile üret

Alternatif terminal komutu (imzalama ayarı sonrası):

```bash
cd android
./gradlew bundleRelease
```

Üretilen dosya:

`android/app/build/outputs/bundle/release/app-release.aab`

## Oyun Kontrolleri

- Ekrana dokun: İç / dış yörünge arasında anında geçiş.
- Sağ üstteki buton: Duraklat.
- Oyun bitince: Reklam izleyip 1 kez devam etme seçeneği.

## Yayınlama Notları (Google Play)

- Paket adı: `com.phaseloop.game` (gerekirse `capacitor.config.ts` içinde değiştir).
- Gizlilik politikası URL'si hazırlayın.
- İçerik derecelendirmesi ve veri güvenliği formunu doldurun.
- Banner/Interstitial/Rewarded şu an simülasyon. Gerçek AdMob için native SDK entegrasyonu gerekir.
