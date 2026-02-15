# Phase Loop

Tek dosyalı HTML5 mobil oyun (Canvas + Vanilla JS). Android'e paketlemek için Capacitor tabanlı kurulum dosyaları repo içinde hazırlandı.

## İçerik

- `index.html`: Oyunun tüm kodu (UI, oyun döngüsü, ses, titreşim, reklam simülasyonu, localStorage).
- `package.json`: Gerekli npm bağımlılıkları ve komutlar.
- `capacitor.config.json`: Android uygulama kimliği ve proje ayarları.

## Android AAB Alma (Adım Adım)

> Gereksinimler: Node.js 18+, Android Studio (SDK + Build Tools), Java 17.

1. Bağımlılıkları kur:

```bash
npm install
```

2. Android platformunu oluştur (ilk kurulumda):

```bash
npm run cap:add:android
```

3. Web dosyalarını Android projesine senkronla:

```bash
npm run cap:sync
```

4. Android Studio ile aç:

```bash
npm run android
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

Windows PowerShell için:

```powershell
cd android
.\gradlew.bat bundleRelease
```

Üretilen dosya:

`android/app/build/outputs/bundle/release/app-release.aab`

## Sık Yapılan Hatalar ve Çözümler

### 1) `Could not find installation of TypeScript`
Bu repoda artık `capacitor.config.json` kullanılıyor. Ekstra TypeScript kurulumu gerekmez.

### 2) `npm cap add android` hatası
Doğru komut **npm değil npx/capacitor scriptidir**:

```bash
npm run cap:add:android
```

veya

```bash
npx cap add android
```

### 3) Yanlışlıkla `npm add android` çalıştırdım
Bu komut npm'e gereksiz `android` paketi ekler. Geri almak için:

```bash
npm uninstall android
```

### 4) `deprecated` uyarıları
`npm warn deprecated ...` mesajları çoğunlukla dolaylı bağımlılıklardan gelir. Uygulamayı genelde engellemez.

### 5) `npm audit` yüksek açıklar
Önce güvenli güncelleme deneyin:

```bash
npm audit fix
```

`npm audit fix --force` kırıcı değişiklik yapabilir; üretimden önce test ederek kullanın.

## Oyun Kontrolleri

- Ekrana dokun: İç / dış yörünge arasında anında geçiş.
- Sağ üstteki buton: Duraklat.
- Oyun bitince: Reklam izleyip 1 kez devam etme seçeneği.

## Yayınlama Notları (Google Play)

- Paket adı: `com.phaseloop.game` (gerekirse `capacitor.config.json` içinde değiştir).
- Gizlilik politikası URL'si hazırlayın.
- İçerik derecelendirmesi ve veri güvenliği formunu doldurun.
- Banner/Interstitial/Rewarded şu an simülasyon. Gerçek AdMob için native SDK entegrasyonu gerekir.
