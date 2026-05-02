<h1 align="center">☀️ Pollution Impact on Solar Energy Generation (Bali)</h1>

<p align="center">
  <em>Sistem analisis, pemodelan, dan simulasi dampak polusi udara terhadap kinerja dan efisiensi panel surya (Photovoltaic).</em>
</p>

<hr>

<h2 align="left">📖 Tentang Proyek Ini</h2>
<p align="justify">
  Proyek <strong><code>PollutionImpactOnSolar</code></strong> adalah sebuah sistem berbasis Python yang dirancang untuk menganalisis dan mengkuantifikasi seberapa besar kerugian efisiensi yang dialami oleh panel surya akibat polusi udara. Berdasarkan struktur modulnya, proyek ini difokuskan pada studi kasus di wilayah <strong>Bali</strong>. 
</p>
<p align="justify">
  Program ini berjalan secara <em>end-to-end</em>, mulai dari pengumpulan data mentah kondisi atmosfer (cuaca dan polutan), pemrosesan simulasi daya energi surya, hingga visualisasi hasil analisis melalui sebuah sistem <em>dashboard</em> interaktif.
</p>

<br>

<h2 align="left">📊 Jenis Data & Proses ETL</h2>
<p align="justify">
  Sistem ini mengelola beberapa sumber data yang berbeda dan mengintegrasikannya menggunakan <em>pipeline</em> ETL (<strong>Extract, Transform, Load</strong>) tersendiri agar dapat dibaca oleh algoritma simulasi.
</p>

<h3 align="left">🗂️ Jenis Data yang Digunakan:</h3>
<ul>
  <li>
    <strong>Data Kualitas Udara (Polusi):</strong> Diambil dan dikelola melalui modul <code>openaqbali.py</code>. Modul ini bertugas menarik parameter polutan udara secara dinamis (seperti PM2.5, PM10) melalui API.
  </li>
  <li>
    <strong>Data Meteorologi (Cuaca):</strong> Dikelola oleh modul <code>meteobali.py</code>. Data ini mencakup parameter atmosfer yang memengaruhi besaran radiasi matahari, seperti suhu, kelembapan, dan persentase tutupan awan.
  </li>
  <li>
    <strong>Data Simulasi PV:</strong> Dihasilkan oleh modul <code>pv_simulation.py</code>, yang berisi model matematis/fisika untuk menghitung seberapa banyak energi listrik (Watt) yang mampu diproduksi oleh panel surya berdasarkan parameter cuaca dan tingkat polusi saat itu.
  </li>
</ul>

<h3 align="left">⚙️ Alur Kerja ETL (<code>pv_etl_pipeline.py</code>):</h3>
<p align="justify">
  Proses otomatisasi data dijalankan dengan tahapan sebagai berikut:
</p>
<ol>
  <li>
    <strong>Extract:</strong> Menarik <em>raw data</em> dari berbagai sumber (API cuaca dan kualitas udara) pada rentang waktu tertentu.
  </li>
  <li>
    <strong>Transform:</strong> Membersihkan data dari nilai kosong (<em>null</em>), menyelaraskan zona waktu (<em>timestamp</em>), dan menggabungkan variabel polusi dengan metrik cuaca agar menjadi satu dataset komprehensif.
  </li>
  <li>
    <strong>Load:</strong> Memuat hasil data yang sudah bersih dan terstruktur ke dalam penyimpanan final, yang selanjutnya divisualisasikan oleh modul antarmuka <code>dashboardbali_upgrade.py</code>.
  </li>
</ol>

<br>

<h2 align="left">🚨 Urgensi Pembuatan Proyek</h2>
<p align="justify">
  Dalam operasional Pembangkit Listrik Tenaga Surya (PLTS), keberadaan partikel debu dan polutan di udara dapat menghalangi datangnya radiasi matahari (<em>atmospheric scattering</em>) atau menumpuk pada permukaan panel (<em>soiling effect</em>). Urgensi dan tujuan utama dari proyek ini meliputi:
</p>
<ul>
  <li>
    <strong>Akurasi Prediksi Daya:</strong> Prediksi produksi energi sering kali meleset (<em>overestimate</em>) jika hanya mengandalkan prediksi cuaca cerah tanpa memperhitungkan kabut/jerebu akibat polusi. Sistem ini memberikan estimasi yang jauh lebih realistis.
  </li>
  <li>
    <strong>Optimalisasi Jadwal <em>Maintenance</em>:</strong> Dengan melacak tren polusi, operator PLTS dapat memprediksi tingkat kekotoran panel surya. Hal ini memungkinkan penjadwalan pembersihan panel secara presisi guna mencegah penurunan daya dan memangkas biaya operasional.
  </li>
  <li>
    <strong>Perencanaan Energi Berkelanjutan:</strong> Khusus untuk wilayah pariwisata ekologis seperti Bali, analisis ini sangat vital bagi para pembuat kebijakan maupun investor dalam menghitung kelayakan ekonomi infrastruktur energi surya di tengah dinamika kualitas udara lokal.
  </li>
</ul>

<hr>

<p align="center">
  <small>Dibuat untuk kebutuhan analisis data spasial, teknik sistem tertanam, dan pelestarian energi terbarukan.</small>
</p>
