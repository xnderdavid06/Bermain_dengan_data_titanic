# 🛳️ Bermain-dengan-data-titanic

## 🔹 Analisis Variabel Baru: Lansia (is_elderly)

Variabel **is_elderly** dibuat berdasarkan umur (`age`) untuk mengklasifikasikan penumpang apakah termasuk lansia atau tidak:  

- `is_elderly = 1` → Lansia (usia ≥ 60 tahun)  
- `is_elderly = 0` → Tidak Lansia (usia < 60 tahun)  

```python
# Import library
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# 1. Memuat Dataset Titanic
titanic = sns.load_dataset('titanic')

# 2. Membuat variabel 'is_elderly'
titanic['is_elderly'] = (titanic['age'] >= 60).astype(int)

# 3. Menampilkan beberapa baris pertama
print("\nDataset dengan Kolom 'age' dan 'is_elderly':")
print(titanic[['age', 'is_elderly']].head(10))

# 4. Visualisasi distribusi variabel 'is_elderly'
plt.figure(figsize=(8, 6))
sns.countplot(x='is_elderly', data=titanic, palette='viridis')
plt.title("Distribusi Penumpang Lansia vs Tidak Lansia")
plt.xlabel("Tidak Lansia (0) / Lansia (1)")
plt.ylabel("Jumlah Penumpang")
plt.show()

# 5. Visualisasi survival rate berdasarkan 'is_elderly'
plt.figure(figsize=(8, 6))
sns.barplot(x='is_elderly', y='survived', data=titanic, palette='viridis')
plt.title("Tingkat Kelangsungan Hidup: Lansia vs Tidak Lansia")
plt.xlabel("Kategori Penumpang")
plt.ylabel("Tingkat Kelangsungan Hidup (Survival Rate)")
plt.xticks([0, 1], ['Tidak Lansia (<60)', 'Lansia (>=60)'])
plt.show()

# 6. Menampilkan ringkasan data
print("\n📊 Ringkasan Data Lansia vs Tidak Lansia:")
summary = pd.DataFrame({
    "Jumlah Penumpang": titanic['is_elderly'].value_counts().rename(index={0: 'Tidak Lansia (<60)', 1: 'Lansia (>=60)'}),
    "Rata-rata Kelangsungan Hidup": titanic.groupby('is_elderly')['survived'].mean().rename(index={0: 'Tidak Lansia (<60)', 1: 'Lansia (>=60)'})
})
print(summary)

# 7. Visualisasi proporsi (Pie Chart)
plt.figure(figsize=(6, 6))
plt.pie(
    summary["Jumlah Penumpang"],
    labels=summary.index,
    autopct='%1.1f%%',
    startangle=90,
    colors=['#66c2a5', '#fc8d62']
)
plt.title("Proporsi Penumpang Lansia vs Tidak Lansia")
plt.show()
