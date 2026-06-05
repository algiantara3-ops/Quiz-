# Quiz-


---

## 📝 Jawaban Quis 1 Struktur Data

### 1. Karakteristik Memori dan Akses Data
**Mengapa akses Array O(1), sedangkan Singly Linked List O(n)?**

| Aspek | Array | Singly Linked List |
|-------|---------|-------------------|
| **Alokasi Memori** | Kontigu (berurutan) | Non-kontigu (tersebar) |
| **Mekanisme Akses** | Menggunakan rumus alamat: `Alamat[i] = Alamat_Dasar + i * Ukuran_Tipe_Data`. Komputer bisa langsung menghitung lokasi elemen mana pun secara matematis. | Harus traversing dari `head` node ke node berikutnya secara berurutan melalui pointer `next` sampai menemukan indeks yang dituju. |
| **Kompleksitas** | **O(1)** - Akses langsung tanpa iterasi | **O(n)** - Bergantung pada posisi elemen (worst case: elemen di akhir) |

> **Kesimpulan:** Sifat memori kontigu pada Array memungkinkan *random access*, sedangkan Linked List hanya mendukung *sequential access*.

---

### 2. Analisis Efisiensi Operasi Manipulasi
**Kapan Linked List lebih unggul daripada Array untuk Insertion/Deletion?**

Linked List lebih diunggulkan dalam kondisi berikut:

1.  **Operasi di Awal/Tengah Struktur:**
    *   **Array:** Memerlukan *shifting* (pergeseran) elemen-elemen setelah titik insert/delete. Kompleksitas: **O(n)**.
    *   **Linked List:** Cukup mengubah pointer dari node sebelumnya ke node baru/target. Jika node referensi sudah diketahui, kompleksitas: **O(1)**.

2.  **Ukuran Data Sangat Dinamis:**
    *   **Array:** Memerlukan alokasi ulang memori dan copying jika kapasitas penuh (resizable array).
    *   **Linked List:** Alokasi memori bersifat dinamis per node, tidak ada waste memori akibat over-alokasi atau biaya copying besar.

> **Alasan Teoritis:** Linked List memisahkan *logical order* dari *physical memory address*, sehingga manipulasi struktur hanya berupa operasi pointer, bukan manipulasi blok memori massal.

---

### 3. Konsep Doubly Linked List
**Anatomi Node & Dampak Pointer Tambahan:**

```text
Struktur Node Doubly Linked List:
[ prev | data | next ]
```

| Komponen | Fungsi |
|----------|---------|
| `prev` | Pointer ke node sebelumnya |
| `data` | Menyimpan nilai/informasi |
| `next` | Pointer ke node berikutnya |

**Dampak:**
*   ** Fleksibilitas:** Bisa traversing dua arah (maju & mundur). Operasi delete lebih efisien jika hanya diberi referensi node yang akan dihapus (karena bisa akses node sebelumnya lewat `prev`).
*   ** Overhead Memori:** Setiap node membutuhkan memori ekstra untuk menyimpan satu pointer tambahan (`prev`).
*   ** Kompleksitas Kode:** Perlu penanganan lebih hati-hati untuk kedua pointer saat insert/delete agar tidak terjadi *dangling pointer*.

---

### 4. Mekanisme Circular Linked List
**Perbedaan Teoritis & Use Case:**

| Fitur | Linked List Biasa | Circular Linked List |
|-------|------------------|---------------------|
| **Node Terakhir** | Pointer `next` bernilai `NULL` | Pointer `next` menunjuk kembali ke `head` (atau node pertama) |
| **Alur Traversal** | Linear (berhenti di akhir) | Siklik/Melingkar (tidak ada akhir mutlak) |

**Contoh Use Case Efektif:**
🎮 **Sistem Round-Robin Scheduling pada OS**
Setiap proses dalam antrian CPU dihubungkan secara melingkar. Setelah proses terakhir selesai menjalankan time slice-nya, scheduler langsung kembali ke proses pertama tanpa perlu reset pointer ke head, membuat siklus penjadwalan lebih efisien dan natural.

---

### 5. Array Dinamis di Python
**Mekanisme "Di Balik Layar" Saat Append Melebihi Kapasitas:**

Python `list` adalah implementasi *Dynamic Array*. Saat kapasitas internal penuh dan dilakukan `.append()`:

1.  **Deteksi Penuh:** Sistem memeriksa bahwa `size == capacity`.
2.  **Alokasi Baru:** Alokasi blok memori baru yang lebih besar. Strategi umum: *growth factor* ~1.125 (Python) atau 2x (implementasi lain).
    *   *Contoh:* Kapasitas 8 → 9, atau 8 → 16.
3.  **Copy Elemen:** Menyalin semua elemen dari array lama ke array baru (operasi **O(n)**).
4.  **Dealokasi:** Memori array lama dibebaskan (garbage collection).
5.  **Insert:** Elemen baru ditambahkan ke slot yang tersedia.

> **Catatan Kompleksitas:** Meskipun operasi resize bersifat O(n), karena kejadian ini jarang (amortized), kompleksitas rata-rata operasi `.append()` tetap **O(1) Amortized**.

---

