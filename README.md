# FamilyCash

Aplikasi catatan keuangan keluarga (Suami, Istri, Anak 1, Anak 2) dengan laporan PDF & Excel.
Satu file `index.html`, data disimpan di Firebase Firestore, login memakai Firebase Auth (email + kata sandi).

## Pasang (sekali saja)
1. Firebase Console → proyek **familycash-79ce4**
2. **Build → Authentication → Sign-in method** → aktifkan **Email/Password**.
   Lalu tab **Users → Add user** untuk tiap anggota keluarga (suami, istri).
   (Opsional tapi disarankan: Settings → User actions → matikan pendaftaran mandiri.)
3. **Build → Firestore Database → Create database** (mode production).
4. Buka `firestore.rules`, ganti email di daftar dengan email anggota keluarga, lalu salin isinya ke tab **Rules** di Firestore → **Publish**
   (atau `firebase deploy --only firestore:rules`).
5. Hosting:
   ```
   npm i -g firebase-tools
   firebase login
   firebase deploy --only hosting --project familycash-79ce4
   ```
   Alamat: https://familycash-79ce4.web.app (domain ini otomatis diizinkan untuk login).
   Jika memakai GitHub Pages / domain lain, tambahkan domainnya di Authentication → Settings → Authorized domains.

## Struktur data
- `tx/{id}`: `{t:'in'|'out', d:'YYYY-MM-DD', a:jumlah, w:'0-3' (anggota), c:'0-2' (kategori, pengeluaran), k:keterangan}`
- `settings/main`: `{names:[4 nama], cats:[3 kategori]}`

Catatan: `apiKey` Firebase untuk web bukan rahasia; keamanan data ditentukan oleh **aturan Firestore** di atas.
