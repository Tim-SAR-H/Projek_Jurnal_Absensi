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

| Login | Register | Home | List Mahasiswa |
|---|---|---|---|
| <img width="2880" height="1800" alt="Login" src="https://github.com/user-attachments/assets/2e0ffc8d-2a14-4cf8-8500-65e311e2ad44" /> | <img width="2880" height="1800" alt="Buat Akun" src="https://github.com/user-attachments/assets/06d5ebfe-dc22-42a7-a54f-d759503cf27f" /> | <img width="2880" height="1800" alt="Home" src="https://github.com/user-attachments/assets/b675a144-ca56-4581-893b-986332241ed0" /> | <img width="2880" height="1800" alt="Daftar Mahasiswa" src="https://github.com/user-attachments/assets/a972d168-b7ec-4709-9b77-6f76291f744f" /> |

| Creat | Edit | Delete |
|---|---|---|
| <img width="2880" height="1800" alt="Creat Data" src="https://github.com/user-attachments/assets/5149970c-558a-4c38-a04f-7befc720f9a0" /> | <img width="2880" height="1800" alt="Edit Data" src="https://github.com/user-attachments/assets/7785976a-f717-427f-a1e8-623cd90ed442" /> | <img width="2880" height="1800" alt="Delete Data" src="https://github.com/user-attachments/assets/5fbb722a-6797-447f-b0da-53cd87074379" /> |

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

## 🔗 Video Presentasi

- [📁 Google Drive]([[https://drive.google.com/drive/folders/FOLDER_ID](https://drive.google.com/drive/folders/17JrUx3zqubZNeFm8PP4xlk9Lfozna0XS?usp=sharing)](https://drive.google.com/drive/folders/17JrUx3zqubZNeFm8PP4xlk9Lfozna0XS?usp=sharing)
