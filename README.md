# Ferryman Reader

A page-by-page translator for manga, PDFs, and HTML/text files. Each page is
translated only when you open it, so nothing is translated in bulk up front.

- **Manga**: pick all the page images for a chapter — OCR (Tesseract.js) reads
  the text, then it's translated.
- **PDF**: pulls real text per page (works best on text-based PDFs, not scans).
- **HTML/TXT**: split into chunks and translated as you read.

The web app lives in `www/index.html`. `android/` is a Capacitor-wrapped
Android project that shows that same page inside a native WebView shell.

## Run it as a website

Just open `www/index.html` in a browser, or host the `www/` folder anywhere
static (GitHub Pages, Netlify, etc).

## Get the Android APK

A GitHub Actions workflow (`.github/workflows/build-android.yml`) builds a
debug APK automatically on every push to `main`. After pushing:

1. Go to your repo's **Actions** tab.
2. Open the latest **Build Android APK** run.
3. Download the `ferryman-reader-debug-apk` artifact — it contains
   `app-debug.apk`. Copy it to your phone and install it (you'll need to allow
   "install from unknown sources" the first time).

## Build the APK yourself instead (optional)

You'll need Node.js, and Android Studio (or just the Android SDK + Java 17)
installed locally.

```bash
npm install
npx cap sync android
cd android
./gradlew assembleDebug
```

The APK will be at `android/app/build/outputs/apk/debug/app-debug.apk`.

## Notes / limitations

- Translation uses a free public API, so heavy use may get rate-limited.
- OCR and translation both need an internet connection.
- Reading progress and translated pages are cached locally on-device, but the
  original uploaded files themselves aren't — you'll re-add the same file(s)
  to resume, and cached translations will load instantly.
