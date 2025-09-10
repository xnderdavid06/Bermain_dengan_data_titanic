# 🚢 Analisis Titanic: Lansia vs Tidak Lansia

## 📌 Deskripsi
Proyek ini menganalisis data Titanic dengan fokus pada variabel baru **Lansia (is_elderly)**.  
Variabel ini dibuat dari kolom `age` untuk mengklasifikasikan penumpang berdasarkan umur:

- **is_elderly = 1** → Lansia (usia ≥ 60 tahun)  
- **is_elderly = 0** → Tidak Lansia (usia < 60 tahun)  

Tujuan analisis ini adalah melihat **perbedaan jumlah penumpang dan survival rate** antara lansia dan tidak lansia.

---

## 📊 Kode Analisis

```python
# Import library
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Memuat Dataset Titanic
titanic = sns.load_dataset('titanic')

# 2. Membuat variabel baru: is_elderly
titanic['is_elderly'] = (titanic['age'] >= 60).astype(int)

# 3. Membuat tabel gabungan jumlah penumpang & survival rate
summary_table = titanic.groupby('is_elderly').agg(
    Jumlah_Penumpang=('survived', 'count'),
    Survival_Rate=('survived', 'mean')
).rename(index={0: 'Tidak Lansia (<60)', 1: 'Lansia (>=60)'})

print("\n📊 Ringkasan Analisis:")
print(summary_table)

# 4. Visualisasi Survival Rate
plt.figure(figsize=(8, 6))
sns.barplot(x='is_elderly', y='survived', data=titanic, palette='viridis')
plt.title('Tingkat Kelangsungan Hidup: Lansia vs Tidak Lansia', fontsize=16)
plt.xlabel('Kategori Penumpang', fontsize=12)
plt.ylabel('Tingkat Kelangsungan Hidup (Survival Rate)', fontsize=12)
plt.xticks([0, 1], ['Tidak Lansia (<60)', 'Lansia (>=60)'])
plt.tight_layout()
plt.savefig("data_titanic.png")  # simpan hasil visualisasi
plt.show()
