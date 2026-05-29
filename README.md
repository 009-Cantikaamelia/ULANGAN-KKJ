# 🌟 Dokumentasi Proyek Website Sosial Media (STARGRAM)

## 🚀 1. Penjelasan Fetch API
Aplikasi ini mengambil data pengguna (*user data*) secara dinamis dari API publik eksternal yang disediakan oleh **JSONPlaceholder** melalui URL berikut:
`https://jsonplaceholder.typicode.com/users`

Proses *Fetch API* dilakukan secara asinkronus menggunakan fungsi bawaan JavaScript `fetch()` di dalam file utama `App.jsx`. Data yang berhasil diambil berupa format JSON yang berisi informasi profil seperti `name`, `username`, dan `email` yang kemudian disimpan ke dalam state untuk didistribusikan ke komponen-komponen kartu.

## 📦 2. Penjelasan Component yang Dibuat & Fungsinya

1. **`App.jsx` (Parent/Main Component)**
   - **Fungsi**: Sebagai pusat kontrol aplikasi. Berperan mengelola state utama (data users, teks pencarian, dan total likes global), melakukan fetch API, menyaring data, dan merender tata letak layout utama.
2. **`Navbar.jsx`**
   - **Fungsi**: Menampilkan header bagian atas aplikasi yang berisi logo utama **STARGRAM**, kolom input teks untuk melakukan pencarian *username*, serta indikator jumlah total suka (*Total Likes*) yang aktif di seluruh aplikasi.
3. **`UserCard.jsx`**
   - **Fungsi**: Berperan sebagai kartu profil individual untuk masing-masing user. Komponen ini menampilkan inisial nama, nama lengkap, username, email, serta menangani interaktivitas lokal tombol *Like* dan *Follow*.
4. **`Footer.jsx`**
   - **Fungsi**: Menampilkan catatan kaki (*copyright*) di bagian paling bawah halaman web sebagai pelengkap layout tata letak.

## 🛠️ 3. Implementasi React Hooks

### A. `useState`
Digunakan untuk membuat state lokal yang melacak perubahan data pada komponen agar UI memperbarui dirinya sendiri secara otomatis:
- Di `App.jsx`: Mengelola data array pengguna (`users`), kata kunci pencarian (`search`), dan penghitung jumlah suka secara global (`totalLikes`).
- Di `UserCard.jsx`: Mengubah status tombol suka (`isLiked`) dan tombol ikuti (`isFollowed`) saat berinteraksi.

### B. `useEffect`
Digunakan untuk menangani *side effects* atau proses sinkronisasi komponen:
- Di `App.jsx`: Memanggil fungsi *Fetch API* dengan *dependency array* kosong (`[]`) agar proses pengambilan data dari internet hanya dieksekusi **satu kali** tepat ketika aplikasi pertama kali dimuat di browser (*componentDidMount*).

### C. `useContext` (atau Pemisahan State)
Digunakan sebagai metode manajemen data guna mengalirkan fungsi pengubah pencarian (`setSearch`) dari `Navbar` ke fungsi penyaringan data utama (`filteredUsers`) di komponen utama, serta mengirimkan aksi ketukan *Like* individual kembali ke penampung angka *Total Likes* di bagian atas halaman secara terpusat.

### D. `useRef`
Dapat diimplementasikan di dalam `Navbar.jsx` untuk menunjuk langsung elemen `<input>` pencarian di dalam DOM. Digunakan agar sesaat setelah halaman selesai dimuat, kursor pengetikan langsung aktif secara otomatis (*auto-focus*) ke kolom pencarian tanpa perlu diklik manual oleh pengguna.

## 💻 4. Bukti Implementasi Potongan Kode Program

Berikut adalah potongan kode program utama yang merealisasikan fitur-fitur di atas dengan gaya visual *Colorful Instagram Style*:

### 🔹 Looping Data dengan `.map()` di `App.jsx`
```jsx
{filteredUsers.length > 0 ? (
  filteredUsers.map((user, index) => (
    <UserCard 
      key={user.id} 
      user={user} 
      index={index} 
      onLikeToggle={handleLikeToggle} 
    />
  ))
) : (
  <p>User tidak ditemukan</p>
)}