# 🚢 Analisis Titanic: Lansia vs Tidak Lansia

## 📌 Deskripsi
Proyek ini menganalisis data Titanic dengan fokus pada variabel baru **Lansia (is_elderly)**.  
Variabel ini dibuat dari kolom `age` untuk mengklasifikasikan penumpang berdasarkan umur:

- **is_elderly = 1** → Lansia (usia ≥ 60 tahun)  
- **is_elderly = 0** → Tidak Lansia (usia < 60 tahun)  

Tujuan analisis ini adalah melihat **jumlah penumpang** dan **tingkat kelangsungan hidup (survival rate)** berdasarkan kategori umur.

---

## 📊 Kode Analisis

```python
# Import library
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# 1. Memuat Dataset Titanic
titanic = sns.load_dataset('titanic')

# 2. Membuat variabel 'is_elderly'
titanic['is_elderly'] = (titanic['age'] >= 60).astype(int)

# --- Visualisasi Survival Rate ---
plt.figure(figsize=(8, 6))
sns.barplot(x='is_elderly', y='survived', data=titanic, palette='viridis')

# Tambahkan judul dan label
plt.title('Tingkat Kelangsungan Hidup: Lansia vs Tidak Lansia', fontsize=16)
plt.xlabel('Kategori Penumpang', fontsize=12)
plt.ylabel('Tingkat Kelangsungan Hidup (Survival Rate)', fontsize=12)

# Ubah label sumbu X biar lebih informatif
plt.xticks(ticks=[0, 1], labels=['Tidak Lansia (<60)', 'Lansia (>=60)'])

# Simpan hasil visualisasi ke file PNG
plt.tight_layout()
plt.savefig("data_titanic.png")
plt.show()

# --- Tabel Ringkas ---
print("\n📊 Rata-rata Kelangsungan Hidup:")
print(titanic.groupby('is_elderly')['survived'].mean())

print("\n📊 Jumlah Penumpang per Kategori:")
print(
    titanic['is_elderly'].value_counts().rename(
        index={0: 'Tidak Lansia (<60)', 1: 'Lansia (>=60)'}
    )
)
