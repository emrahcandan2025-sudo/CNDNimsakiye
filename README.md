# CNDN Namaz Vakitleri (Android)

Tek dosyalı HTML uygulaması (`www/index.html`), Capacitor ile Android APK'ya çevrilir.
APK'yı GitHub Actions derler ve **Releases** sayfasına yükler.

## İlk kurulum
1. GitHub'da yeni bir depo oluştur (ör. `cndn-namaz-vakitleri`).
2. Bu klasörün içeriğini depoya yükle (`.github` klasörü dahil).
3. Sürüm etiketi at:
   ```
   git tag v1.0.0
   git push origin v1.0.0
   ```
   (Etiket yerine Actions sekmesinden "APK Release" → "Run workflow" da çalışır.)
4. Birkaç dakika sonra **Releases** sayfasında `CNDN-Namaz-Vakitleri-v1.0.0.apk` görünür.

## Güncelleme yayınlama
`www/index.html` dosyasını değiştir, commit'le ve yeni etiket at (`v1.0.1`, `v1.0.2` ...).

## Sabit imza anahtarı (önerilir)
Varsayılan olarak her derlemede geçici anahtar üretilir; bu durumda yeni APK'yı eskisinin üzerine
güncelleme olarak kuramazsın (önce eskisini silmen gerekir). Sabit anahtar için:
```
keytool -genkeypair -keystore cndn.jks -alias cndn -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 cndn.jks
```
Depo → Settings → Secrets and variables → Actions bölümüne ekle:
- `KEYSTORE_BASE64` (yukarıdaki base64 çıktısı)
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS` (örn. `cndn`)
- `KEY_PASSWORD` (anahtar şifresi; boşsa KEYSTORE_PASSWORD kullanılır)

`cndn.jks` dosyasını depoya yükleme ve kaybetme; Play Store veya güncelleme için gerekir.

## Telefona kurulum
APK'yı indirip aç; "bilinmeyen kaynaklardan yükleme" izni isteyebilir.

## Notlar
- Vakitler cihazda hesaplanır, internet gerekmez (Amiri yazı tipi uygulamanın içinde).
- Vakitler Diyanet tablosundan 1-2 dakika sapabilir.
