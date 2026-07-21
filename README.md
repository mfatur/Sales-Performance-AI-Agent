# Sales-Performance-AI-Agent
An AI-powered retail sales analytics agent built with Langflow that automates data cleaning, KPI calculations, and interactive questio
## Problem Statement

Analisis performa penjualan pada data transaksi berskala besar (puluhan ribu baris, lintas kategori dan wilayah) masih dilakukan secara manual menggunakan spreadsheet atau query teknis, sehingga proses menemukan insight seperti tren penjualan bulanan, kategori paling menguntungkan, atau penyebab penurunan sales memakan waktu lama dan rentan kesalahan interpretasi data.

## Target Users

Pengguna utama solusi ini adalah manajer penjualan/sales manager, business analyst, dan business owner/eksekutif di perusahaan retail atau ritel multi-kategori yang memiliki volume data transaksi cukup besar untuk dianalisis secara berkala.

Karakteristik:

Memiliki kebutuhan tinggi memahami performa bisnis, namun tidak selalu memiliki kemampuan teknis (SQL/Python/Excel kompleks).
Bekerja dengan tekanan waktu, butuh jawaban cepat untuk mendukung keputusan operasional/strategis.
Lebih nyaman bertanya dalam bahasa natural dibanding membaca dashboard teknis.

Kebutuhan:

Ringkasan performa penjualan siap pakai (Executive Summary).
Kemampuan bertanya lebih lanjut (drill-down) tanpa menunggu laporan dari tim data.
Insight yang disertai rekomendasi actionable.

Konteks Penggunaan: Digunakan secara berkala (harian/mingguan/bulanan) saat meninjau performa penjualan terbaru, menyiapkan laporan ke manajemen, atau investigasi cepat atas anomali data.

## Potential Impact

Solusi ini mengotomatiskan seluruh alur analisis data penjualan — dari cleaning data, perhitungan KPI, hingga menjawab pertanyaan analitis secara interaktif melalui LLM. Manfaat utamanya:

Efisiensi waktu — proses yang sebelumnya berjam-jam kini selesai dalam hitungan detik/menit.
Aksesibilitas tanpa hambatan teknis — insight kompleks bisa digali cukup dengan bertanya dalam bahasa sehari-hari.
Pengambilan keputusan lebih cepat & berbasis data — Executive Summary dan rekomendasi otomatis membantu merespons tren negatif lebih dini.
Konsistensi & akurasi — perhitungan KPI dilakukan programatis, meminimalkan human error.
Skalabilitas — arsitektur berbasis komponen memudahkan pengembangan lebih lanjut.
## 🔄 Alur Sistem

Input: File CSV data transaksi penjualan (Superstore) + pertanyaan pengguna dalam bahasa natural.

Proses: Data CSV dibersihkan (cleaning, cek missing value & duplikat), lalu diolah menjadi KPI (revenue, profit, growth rate, top kategori/produk/region). Hasil KPI diringkas otomatis oleh LLM menjadi Executive Summary, Business Insight, dan Recommendation. Saat pengguna bertanya, Agent memilih dan memanggil tool yang sesuai (query tren waktu atau query dimensi) untuk mengambil data spesifik dari hasil olahan tersebut, lalu LLM menyusun jawabannya.

Output: Ringkasan performa penjualan otomatis serta jawaban interaktif yang akurat dan berbasis data nyata, termasuk drill-down penyebab tren dan rekomendasi actionable.

🛠️ Apa yang Diterapkan di Project Ini
Arsitektur agentic dengan tool-calling — Agent mengambil data KPI langsung dari hasil olahan data transaksi, bukan dari asumsi LLM.
Custom Python component untuk data cleaning, perhitungan KPI, serta 2 tools terpisah:
Trend Query Tool — analisis time-series (growth rate & drill-down penyebab perubahan sales per kategori/region).
Dimension Query Tool — query dimensi (top produk, kategori, customer, region).
Prompt engineering terstruktur dengan batasan data eksplisit di dalam prompt, agar LLM tidak menghasilkan insight yang menyesatkan (hallucination) di luar cakupan data.
Agent instructions dengan guardrail untuk mencegah tool-calling berulang tanpa henti (infinite loop).
Konversi tipe data antar komponen (Data ↔ Message) agar seluruh pipeline saling terhubung sesuai kebutuhan tipe input/output.
Visualisasi chart tren sales bulanan sebagai gambar di dalam chat, bukan cuma teks.
