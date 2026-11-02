# Jurnal Absensi Mahasiswa

> **UTS Pemrograman Multi Platform Lanjutan (IT312)**  
> Fakultas Teknologi Informasi — Institut Sains dan Bisnis Atma Luhur Pangkalpinang  
> Dosen Koordinator: Rezky Yuranda, M.Kom | Kelompok: **TA5J**

Aplikasi Flutter untuk mencatat absensi mahasiswa (tema **6. Jurnal Absensi/Kelas**) dengan Firebase Auth, Cloud Firestore, Provider, dan REST API Dio.

---

## 👥 Anggota Kelompok & Pembagian Peran

| No | Nama Mahasiswa | NIM | Peran Baku |
|---|---|---|---|
| 1 | **Sandi Kurniawan** | **2411500011** | **main.dart + models folder** |
| 2 | **Hafizh Risqullah Iskandarsyah** | **2411500014** | **providers folder** |
| 3 | **Rezaldi Pratama** | **2411500005** | **screens folder** |
| 4 | **Anugrah Akbar** | **2411500039** | **service folder + theme folder** |

Rincian berkas per anggota:

| Anggota | Berkas yang dikerjakan |
|---|---|
| Sandi Kurniawan | `main.dart`, `models/journal_model.dart`, `models/user_model.dart` |
| Hafizh Risqullah Iskandarsyah | `providers/auth_provider.dart`, `providers/journal_provider.dart`, `providers/data_provider.dart`, `providers/view_state.dart` |
| Rezaldi Pratama | `screens/login_screen.dart`, `screens/home_screen.dart`, `screens/user_list_screen.dart`, `screens/user_detail_screen.dart` |
| Anugrah Akbar | `services/firestore_service.dart`, `services/api_service.dart`, `theme/app_theme.dart` |

---

## 🚀 Fitur Aplikasi

**1. Firebase Authentication**
- Register, login, dan logout (email & password).
- Auth gating reaktif memakai `Stream<User?>` (`authStateChanges()`).
- Pesan error berbahasa Indonesia.

**2. Cloud Firestore CRUD Realtime**
- Collection `journals` dengan field `{nim, status, note, createdAt}` (`createdAt` bertipe `Timestamp`).
- Create, Read (`snapshots()` realtime dan `get()` sekali ambil), Update, dan Delete dengan dialog konfirmasi.
- Tanpa `orderBy()` di query Firestore; pengurutan (terbaru di atas) dan filter status dilakukan di sisi client (Dart).

**3. MultiProvider & ViewState**
- 3 `ChangeNotifier` di `main.dart`: `AuthProvider`, `JournalProvider` (Firestore), `DataProvider` (Dio).
- `ViewState`: `initial`, `loading`, `loaded`, `empty`, `error`.
- Subscription stream dibatalkan di `dispose()` untuk mencegah memory leak.

**4. REST API Dio (read-only)**
- Data mahasiswa dari Reqres (`https://reqres.in/api/users`) dengan header `x-api-key`.
- Timeout koneksi dan terima data masing-masing 10 detik.
- Tampilan loading spinner, empty state, dan error dengan tombol *Retry*.

**5. Navigasi 4 Layar**

| Layar | Berkas | Fungsi |
|---|---|---|
| 1. Login/Register | `login_screen.dart` | Autentikasi dengan toggle masuk/daftar |
| 2. Home CRUD | `home_screen.dart` | Statistik kehadiran, filter status, daftar jurnal, tambah/edit/hapus |
| 3. List API | `user_list_screen.dart` | Daftar mahasiswa dari API, juga dipakai sebagai *picker* NIM |
| 4. Detail API | `user_detail_screen.dart` | Profil mahasiswa, catat absensi cepat, riwayat absensi dari Firestore |

---

## 📸 Screenshot

| Login | Home CRUD | List API | Detail API |
|---|---|---|---|
| *(tempel gambar)* | *(tempel gambar)* | *(tempel gambar)* | *(tempel gambar)* |

> Simpan gambar di folder `screenshots/` lalu tampilkan dengan `![Login](screenshots/login.png)`.

---

## 📁 Struktur Folder

```text
lib/
├── firebase_options.dart         # Konfigurasi Firebase (wajib di-commit)
├── main.dart                     # Init Firebase, MultiProvider, auth gating
├── models/
│   ├── journal_model.dart        # {nim, status, note, createdAt}
│   └── user_model.dart           # Data Reqres {id, email, nama, avatar}
├── providers/
│   ├── auth_provider.dart        # State autentikasi
│   ├── data_provider.dart        # State REST API Dio + ViewState
│   ├── journal_provider.dart     # CRUD Firestore, stream, ViewState
│   └── view_state.dart           # enum ViewState
├── screens/
│   ├── home_screen.dart
│   ├── login_screen.dart
│   ├── user_detail_screen.dart
│   └── user_list_screen.dart
├── services/
│   ├── api_service.dart          # Dio + penanganan error
│   └── firestore_service.dart    # Operasi Firestore
└── theme/
    └── app_theme.dart            # Tema global & warna badge status
```

---

## 🛠️ Cara Menjalankan Aplikasi

Prasyarat: Flutter SDK **>= 3.27** dan koneksi internet.

```bash
# 1. Unduh dependensi
flutter pub get

# 2. (Opsional) Hubungkan ke project Firebase sendiri
dart pub global activate flutterfire_cli
firebase login
flutterfire configure

# 3. Jalankan aplikasi
flutter run
```

> `lib/firebase_options.dart` sudah disertakan di repositori dan **tidak masuk `.gitignore`**, sehingga aplikasi bisa langsung dijalankan. Langkah `flutterfire configure` hanya diperlukan bila ingin memakai project Firebase lain.

Pastikan **Email/Password** sudah diaktifkan di Firebase Console → Authentication → Sign-in method, dan Firestore sudah dibuat.

---

## 💡 Future vs Stream (P01)

| Pembeda | `Future` | `Stream` |
|---|---|---|
| Nilai | **Satu** nilai (atau error), lalu selesai | **Banyak** nilai berkelanjutan sampai di-cancel |
| Di proyek ini | `ApiService.fetchUsers()` (Dio GET), `FirestoreService.getJournalsOnce()` (`get()`) | `authStateChanges()`, `FirestoreService.streamJournals()` (`snapshots()`) |
| Kapan dipakai | Ambil data API sekali / tombol refresh | Jurnal absensi yang berubah secara realtime |

---

## 🔗 Video Presentasi

- **Link Google Drive**: `[MASUKKAN_LINK_GOOGLE_DRIVE_DI_SINI]`

*(Atur akses ke "Siapa saja yang memiliki link dapat melihat".)*
