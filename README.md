## 1. Informasi Umum Studi Kasus
- **Kasus Dipilih:** Case 06 - Traffic Accident Severity Analysis
- **Sektor:** Smart City / Keselamatan Lalu Lintas
- **File Dataset Asli:** `data/case6_traffic_accident.xlsx` (3.000 baris × 17 kolom)
- **Jenis Tugas:** Klasifikasi Multi-Kelas (`tingkat_keparahan`: Ringan, Sedang, Berat)

---

## 2. Ringkasan Temuan Bisnis (Actionable Insights)

1. **Peningkatan Manajemen Risiko Penglihatan Malam & Cuaca Ekstrem:**
   - **Temuan:** Kombinasi cuaca buruk (hujan lebat atau berkabut) pada malam hari menghasilkan persentase keparahan kecelakaan **Berat** paling tinggi (mencapai >45%).
   - **Tindakan:** Pasang rambu peringatan cuaca otomatis (*Variable Message Signs*) dan tingkatkan pencahayaan jalan umum (PJU) pada titik-titik rawan cuaca ekstrem dan kelesuan pandang.

2. **Penegakan Hukum Konsumsi Alkohol pada Pengemudi:**
   - **Temuan:** Pengemudi yang terindikasi mengonsumsi alkohol memiliki proporsi kecelakaan berakibat **Berat** sebesar 43,14%, jauh lebih tinggi dibandingkan pengemudi non-alkohol (26,52%).
   - **Tindakan:** Tingkatkan razia tes kadar alkohol pengemudi (*sobriety checkpoint*) secara rutin pada jam-jam rawan (malam hingga dini hari).

3. **Pengawasan Kecepatan di Ruas Jalan Arteri & Tol:**
   - **Temuan:** Meskipun tingkat kecelakaan tinggi di Jalan Desa, keparahan berakibat Berat terkonsentrasi pada Jalan Kota (32,11%) dan Jalan Tol (30,57%) akibat batas kecepatan yang relatif tinggi.
   - **Tindakan:** Terapkan pemantauan dan penindakan batas kecepatan (*speed camera / ETLE*) secara lebih ketat di jalan tol dan arteri utama kota.

---

## 3. Ringkasan Hasil Audit & Pembersihan Data

- **Penanganan Duplikat:** 0 duplikat pada `accident_id`.
- **Penanganan Missing Values:** 1.345 nilai kosong pada dataset mentah berhasil dibersihkan hingga menjadi **0 nilai kosong** pada dataset akhir.
  - Imputasi fitur numerik (`jam`, `jumlah_korban`, dll.) menggunakan **Median**.
  - Imputasi fitur kategorikal (`kondisi_cuaca`, `tipe_jalan`, dll.) menggunakan **Modus**.
  - Imputasi fitur `tanggal` menggunakan kombinasi `.bfill()` dan `.ffill()`.
- **Penanganan Outlier & Typo:**
  - Pembersihan penulisan typo string pada `kondisi_cuaca` (seperti karakter `@` dan variasi kapitalisasi).
  - Pembatasan outlier (*outlier capping*) pada `jumlah_korban` menggunakan batas IQR per grup `tipe_jalan`.
