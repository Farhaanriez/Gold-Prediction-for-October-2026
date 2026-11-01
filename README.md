# Peramalan Harga Emas: Naive vs Linear Regression vs Random Forest

## Tujuan
Membandingkan model peramalan harga emas harian (USD, Close) dengan
fitur lag 1-3 hari, dan menguji apakah model ML mengalahkan baseline naive.

## Data
- Sumber: [Yahoo Finance, GC=F]
- Latih: Jan-Sep 2026 (184 baris) | Uji: Oktober 2026 (22 hari)
- Split berdasarkan waktu (bukan acak) untuk menghindari data leakage

## Metode
1. Naive: harga hari ini = harga kemarin
2. Linear Regression pada harga (lag_1..3)
3. Random Forest pada harga (lag_1..3)
4. Linear Regression pada selisih harian (memprediksi perubahan)

## Hasil (data uji Oktober 2026)
| Model | MAE | RMSE |
|---|---|---|
| Naive | 37.52 | 48.00 |
| Linear Regression (harga) | 38.13 | 51.58 |
| Random Forest | 44.18 | 56.06 |
| Linear Regression (selisih) | 35.40 | 47.40 |

Akurasi arah: LR 40.9%, RF 54.5% (22 titik uji).

## Temuan
- Model pada harga hampir tidak berbeda dari naive (koefisien lag_1 ~0.97).
- Model selisih memberi MAE terendah, namun selisihnya kecil (~2 USD,
  sekitar 0.05% dari harga) dan belum dapat dianggap signifikan.
- Random Forest tidak mampu mengekstrapolasi level harga yang bergeser.

## Keterbatasan
Hanya 22 titik uji, prediksi satu langkah ke depan, tanpa fitur eksternal.

## Cara menjalankan
Buka notebook di Google Colab, unggah gold_usd.csv, pilih Run all.
