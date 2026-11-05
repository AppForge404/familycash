# FamilyCash

Aplikasi catatan keuangan keluarga (Suami, Istri, Anak 1, Anak 2) dengan laporan PDF & Excel.
Satu file `index.html`, data disimpan di Firebase Firestore, login memakai PIN (Firebase Auth).

## Pasang (sekali saja)
1. Firebase Console -> proyek **familycash-79ce4**
2. **Build -> Authentication -> Sign-in method** -> aktifkan **Email/Password**. (Tidak perlu menambah user; login hanya memakai PIN.)
3. **Build -> Firestore Database -> Create database** (mode production).
4. Salin isi `firestore.rules` ke tab **Rules** -> **Publish** (atau `firebase deploy --only firestore:rules`).
5. Deploy: `firebase deploy --only hosting --project familycash-79ce4` -> https://familycash-79ce4.web.app
6. Buka aplikasi, tekan **Pertama kali? Buat PIN**, buat PIN (minimal 6 karakter). Lakukan segera setelah deploy.

PIN adalah kata sandi akun bersama `keluarga@familycash.app` (diperiksa Firebase Auth, bukan hanya di tampilan).
Ganti PIN: Pengaturan -> Ganti PIN. Jika lupa PIN: Authentication -> Users -> akun tersebut -> Reset password / hapus akun, lalu buat PIN lagi.

## Struktur data
- `tx/{id}`: `{t:'in'|'out', d:'YYYY-MM-DD', a:jumlah, w:'0-3' (anggota), c:'0-2' (kategori, pengeluaran), k:keterangan}`
- `settings/main`: `{names:[4 nama], cats:[3 kategori]}`

Catatan: `apiKey` Firebase untuk web bukan rahasia; keamanan data ditentukan oleh **aturan Firestore** di atas.
