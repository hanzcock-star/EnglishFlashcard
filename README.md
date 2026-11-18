# English Flashcard (Android)

Aplikasi kamus flashcard Inggris–Indonesia berbasis teks, offline-first, dengan pengucapan melalui Android Text-to-Speech dan impor/pembaruan file Excel `.xlsx`.

## Fitur yang sudah disiapkan
- Database SQLite lokal; sepuluh kosakata contoh tersedia saat instalasi pertama.
- Flashcard dengan tombol tampil/sembunyikan arti.
- Status hafalan (sudah/belum), filter, pencarian, dan statistik.
- Pengucapan kata dengan Android TTS bahasa Inggris (tidak membutuhkan internet bila data suara English sudah terpasang).
- Import `.xlsx` melalui pemilih dokumen Android.
- Import bersifat upsert berdasarkan kolom `English`: kata baru ditambahkan dan kata yang sudah ada diperbarui; status hafalan dipertahankan untuk entri yang diperbarui.

## Format Excel
Gunakan sheet pertama. Baris pertama adalah header. Kolom wajib: `English`, `Indonesia`. Kolom opsional: `Category`, `Example`, `Translation`.

| English | Indonesia | Category | Example | Translation |
|---|---|---|---|---|
| apple | apel | Noun | I eat an apple. | Saya makan apel. |
| improve | meningkatkan | Verb | I want to improve my English. | Saya ingin meningkatkan bahasa Inggris saya. |

Berkas contoh: `template_kamus.xlsx`.

## Membuka dan membangun APK
1. Instal Android Studio versi yang mendukung Android Gradle Plugin 8.7.3.
2. Buka folder proyek `EnglishFlashcard` di Android Studio.
3. Tunggu Gradle Sync selesai (koneksi internet diperlukan pertama kali untuk mengunduh Android Gradle Plugin dan Kotlin Gradle Plugin).
4. Pastikan Android SDK Platform 35 terpasang.
5. Pilih **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
6. APK debug akan dibuat di `app/build/outputs/apk/debug/app-debug.apk`.

Alternatif terminal dari folder proyek (setelah Gradle tersedia): `gradle assembleDebug`.

## Catatan penting
- Proyek ini adalah source project Android Studio. APK biner belum disertakan karena lingkungan pembuatan saat ini tidak memiliki Android SDK maupun Gradle terpasang, sehingga APK tidak dapat dikompilasi dan diuji di sini.
- Audio memakai mesin TTS perangkat. Untuk benar-benar offline, pasang data suara English (US) atau English (UK) pada pengaturan Text-to-Speech Android terlebih dahulu.
- Import mendukung `.xlsx` standar dengan shared strings atau inline strings pada sheet pertama. File `.xls` lama tidak didukung.
- Saat impor, jangan mengganti nama header wajib `English` dan `Indonesia`.

## Membuat APK tanpa Android Studio (cloud build)
Proyek ini menyertakan workflow GitHub Actions di `.github/workflows/build-apk.yml`.
1. Buat akun GitHub jika belum punya, lalu buat repository baru (misalnya `EnglishFlashcard`).
2. Unggah seluruh isi folder proyek ini ke repository tersebut; pastikan folder `.github/workflows` ikut terunggah.
3. Buka tab **Actions**, pilih workflow **Build Android APK**, lalu tekan **Run workflow** (atau tunggu build berjalan setelah push ke branch `main`).
4. Setelah selesai dengan status hijau, buka hasil run dan unduh artifact **EnglishFlashcard-debug-apk**.
5. Ekstrak ZIP artifact di komputer/HP, lalu pasang `app-debug.apk` di Android. Jika diminta, izinkan instalasi aplikasi dari sumber tersebut.

Build pertama memerlukan internet di server GitHub untuk mengunduh Gradle dan komponen Android. Setelah APK terpasang, fitur belajar dan database berjalan offline. APK debug ini untuk instalasi pribadi/pengujian, bukan rilis Play Store.
