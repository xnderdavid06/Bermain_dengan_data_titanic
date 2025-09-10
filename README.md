# Bermain-dengan-data-titanic  

## Menambahkan variabel baru: Lansia (`is_elderly`)  
Variabel ini dibuat berdasarkan umur (`age`) untuk mengklasifikasikan penumpang apakah termasuk lansia atau tidak.  
Kriteria:  
- `is_elderly = 1` jika umur ≥ 60 tahun  
- `is_elderly = 0` jika umur < 60 tahun  

```python
titanic['is_elderly'] = (titanic['age'] >= 60).astype(int)
```

---

## Menampilkan beberapa baris pertama untuk verifikasi  

```python
print("\nDataset dengan Kolom 'age' dan 'is_elderly':")
print(titanic[['age', 'is_elderly']].head(10))
```

Contoh output akan menampilkan umur penumpang beserta klasifikasi lansianya.  

---

## Membuat tabel ringkas jumlah penumpang lansia vs tidak  

```python
elderly_table = titanic['is_elderly'].value_counts().rename(index={0: 'Tidak Lansia (<60)', 1: 'Lansia (>=60)'})
print("\n📊 Jumlah Penumpang:")
print(elderly_table)
```

Output berupa jumlah penumpang dalam dua kategori: **Tidak Lansia** dan **Lansia**.  

---

## Visualisasi distribusi variabel `is_elderly`  

### Bar Chart  

```python
plt.figure(figsize=(8, 6))
sns.countplot(x='is_elderly', data=titanic, palette='viridis')
plt.title("Distribusi Penumpang Lansia vs Tidak Lansia")
plt.xlabel("Kategori")
plt.ylabel("Jumlah Penumpang")
plt.xticks([0, 1], ['Tidak Lansia (<60)', 'Lansia (>=60)'])
plt.show()
```

Menampilkan distribusi jumlah penumpang lansia vs tidak lansia.  

---

### Pie Chart  

```python
plt.figure(figsize=(6, 6))
plt.pie(
    elderly_table,
    labels=elderly_table.index,
    autopct='%1.1f%%',
    startangle=90,
    colors=['#66c2a5', '#fc8d62']
)
plt.title("Proporsi Penumpang Lansia vs Tidak Lansia")
plt.show()
```

Menampilkan proporsi (persentase) penumpang lansia dan tidak lansia.  

---

📌 Dengan analisis ini, kita bisa melihat:  
- Distribusi jumlah penumpang berdasarkan kategori umur.  
- Persentase lansia dibandingkan total penumpang Titanic.  
