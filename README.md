# StokPanel — Mobil Uygulama Yapım Rehberi
## Capacitor ile Android APK + iOS IPA

---

## 📁 Klasör Yapısı
```
stokpanel-capacitor/
├── www/
│   ├── index.html          ← Web uygulaması (bunu düzenle)
│   └── icons/              ← Uygulama ikonları
│       ├── icon-512.png
│       ├── splash.png
│       └── ...
├── package.json
├── capacitor.config.json   ← Uygulama ID ve ayarlar
└── README.md               ← Bu dosya
```

---

## ✅ ADIM 0 — Gereksinimler

### Hepsini kur:

| Program | İndirme Linki | Zorunlu |
|---------|--------------|---------|
| **Node.js LTS** | https://nodejs.org | ✅ Her platform |
| **Android Studio** | https://developer.android.com/studio | ✅ Android için |
| **JDK 17** | Android Studio ile gelir | ✅ Android için |
| **Xcode** | Mac App Store (sadece Mac) | ✅ iOS için |

> Kurulumları tamamlayınca terminale yaz: `node --version`
> `v18.0.0` veya üstü görünmeli.

---

## 🤖 ANDROID APK — Windows / Mac / Linux

### ADIM 1 — Terminal aç, klasöre gir
```bash
cd stokpanel-capacitor
```

### ADIM 2 — Paketleri yükle
```bash
npm install
```

### ADIM 3 — Android platformu ekle (sadece ilk seferinde)
```bash
npx cap add android
```

### ADIM 4 — Web dosyalarını senkronize et
```bash
npx cap sync android
```

### ADIM 5 — Android Studio'yu aç
```bash
npx cap open android
```

### ADIM 6 — Android Studio'da APK derle
1. Android Studio açılınca **"Gradle sync"** bitmesini bekle (alt çubukta döner)
2. Üst menü: **Build → Build Bundle(s) / APK(s) → Build APK(s)**
3. Derleme biter (2-5 dk), sağ altta bildirim çıkar
4. **"locate"** linkine tıkla → APK dosyası açılır

**APK konumu:**
```
android/app/build/outputs/apk/debug/app-debug.apk
```

### ADIM 7 — Telefona yükle
**WhatsApp / E-posta ile:**
- APK dosyasını kendine gönder → telefonda aç → Yükle

**USB ile:**
```bash
# Telefonda USB hata ayıklama açık olmalı
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

> ⚠️ İlk yüklemede telefon sorarsa:
> **Ayarlar → Güvenlik → Bilinmeyen kaynaklardan yüklemeye izin ver**

---

## 🍎 iOS IPA — SEÇENEK A: Mac'te (Xcode ile)

### Ön koşul: Mac bilgisayar + Xcode kurulu

### ADIM 1-4 aynı (npm install, cap add, cap sync)
```bash
npm install
npx cap add ios
npx cap sync ios
npx cap open ios
```

### ADIM 5 — Xcode'da aç ve derle
1. Xcode açılır → sol üstten hedef cihazı seç (simulator veya gerçek telefon)
2. **Product → Build** (⌘+B)
3. Gerçek cihaza göndermek için: **Product → Run** (⌘+R)

### App Store için:
1. Apple Developer hesabı gerekli ($99/yıl): https://developer.apple.com
2. **Product → Archive** → Distribute App → App Store Connect

---

## ☁️ iOS IPA — SEÇENEK B: Windows'tan Bulut Derleme (ÜCRETSİZ)

Mac'in yoksa bu yöntemi kullan:

### 1. Ionic Appflow (ücretsiz tier)
1. https://ionic.io/appflow adresine git → ücretsiz kayıt
2. GitHub'a projeyi yükle (veya zip olarak import et)
3. **Build → iOS** → IPA indir

### 2. EAS Build (Expo - ücretsiz)
```bash
npm install -g eas-cli
eas build --platform ios
```
- https://expo.dev → ücretsiz hesap aç
- IPA dosyası bulutta derlenir, indirirsin

---

## 🔄 Güncelleme Yapmak

`www/index.html` dosyasını değiştirince sadece şunu çalıştır:
```bash
# Android için
npx cap sync android

# iOS için
npx cap sync ios
```
Android Studio / Xcode'u tekrar açmak gerekmez. Sadece **Run** et.

---

## 🎨 İkon Değiştirme

### Hazır ikonlar: `www/icons/` klasöründe

### Android Studio'da:
1. Sol panelde `app/src/main/res` → sağ tıkla
2. **New → Image Asset**
3. **Icon Type: Launcher Icons** → kendi PNG'ni seç
4. **Finish**

### Xcode'da:
1. `Assets.xcassets` → `AppIcon` → ikonları sürükle bırak

---

## ⚙️ Uygulama Adı / ID Değiştirme

`capacitor.config.json` dosyasını düzenle:
```json
{
  "appId": "com.sirketing.stokpanel",   ← benzersiz ID (ters domain)
  "appName": "StokPanel",               ← uygulama adı
  ...
}
```
Değiştirince `npx cap sync` çalıştır.

---

## ❓ Sık Karşılaşılan Hatalar

### "SDK location not found"
`android/local.properties` dosyasını aç veya oluştur:
```
sdk.dir=C:\\Users\\KULLANICI_ADIN\\AppData\\Local\\Android\\Sdk
```

### "Gradle sync failed"
Android Studio → **File → Invalidate Caches → Invalidate and Restart**

### "Firebase çalışmıyor"
Capacitor uygulamaları `https://` şemasıyla açılır — Firebase bu şemada çalışır.
İnternetin olduğundan emin ol.

### "Bilinmeyen uygulama" uyarısı (Android)
Normal — imzasız (debug) APK kullanıyorsun.
**Yine de yükle** butonuna bas.

---

## 📞 Destek

Sorun yaşarsan terminaldeki hata mesajını kopyalayıp sor.
