[README.md](https://github.com/user-attachments/files/28634911/README.md)
# 24903014_Ilhan_Sahin_pythonfinal
Bu uygulama, kullanıcının aylık gelir ve giderlerini kaydetmesine, analiz etmesine, grafiklerle görselleştirmesine ve CSV / Excel formatında dışa aktarmasına olanak tanır. **Modüler OOP mimarisinde** yazılmıştır.
# 💰 Kişisel Finans ve Harcama Takip Sistemi

**Ders:** BGY210 – Python Programlama II  
**Öğretim Elemanı:** Dr. Öğr. Üyesi Tohid YOUSEFİ  
**Ödev Türü:** Final Projesi (Bireysel)  

---

## 📌 Proje Hakkında

Bu uygulama, kullanıcının aylık gelir ve giderlerini kaydetmesine, analiz etmesine,
grafiklerle görselleştirmesine ve CSV / Excel formatında dışa aktarmasına olanak tanır.
**Modüler OOP mimarisinde** yazılmıştır.

---

## 📁 Proje Yapısı

```
KisiselFinansTakip/
├── main.py               # Ana uygulama & konsol menü döngüsü
├── finans_modeli.py      # Islem ve FinansYoneticisi sınıfları (OOP)
├── islem_yonetimi.py     # Gelir/gider ekleme, listeleme, silme
├── dosya_islemleri.py    # CSV okuma/yazma + aylık özet CSV
├── analiz.py             # Pandas & NumPy analizleri
├── gorsellestirme.py     # Matplotlib grafikleri
├── excel_aktar.py        # openpyxl ile Excel aktarımı (3 sayfa)
├── utils.py              # Yardımcı fonksiyonlar & doğrulama
├── requirements.txt      # Bağımlılıklar
└── README.md             # Bu dosya
```

### Oluşturulan çıktı dosyaları (çalışma sırasında)

| Dosya | Açıklama |
|---|---|
| `islemler.csv` | Tüm gelir & gider kayıtları |
| `aylik_ozet.csv` | Aylık gelir/gider özeti – **otomatik güncellenir** |
| `finans_raporu.xlsx` | 3 sayfalı Excel raporu |
| `grafikler/aylik_cizgi.png` | Aylık çizgi grafiği |
| `grafikler/gelir_gider_bar.png` | Sütun grafiği |
| `grafikler/pasta.png` | Pasta grafiği |

---

## 🚀 Kurulum ve Çalıştırma

```bash
# 1. Bağımlılıkları yükle
pip install -r requirements.txt

# 2. Uygulamayı başlat
python main.py
```

---

## 🧩 Modül Açıklamaları

### `finans_modeli.py` – OOP Katmanı
- **`Islem`** sınıfı: `id, tutar, tarih, aciklama, tip` alanlarını taşır.  
  `__str__`, `__repr__` ve `sozluge_donustur()` metotları tanımlıdır.
- **`FinansYoneticisi`** sınıfı: `gelirler` ve `giderler` listelerini merkezi olarak yönetir;
  `tum_islemler()`, `toplam_gelir()`, `toplam_gider()`, `net_bakiye()` kısayolları sağlar.

### `utils.py` – Yardımcı Fonksiyonlar
| Fonksiyon | Açıklama |
|---|---|
| `yeni_id_olustur(liste)` | Listeden benzersiz ID üretir |
| `benzersiz_id_olustur(gelirler, giderler)` | Çakışmayan global ID |
| `tarih_kontrol(tarih)` | YYYY-MM-DD doğrulaması |
| `sayi_kontrol(deger)` | Pozitif sayı doğrulaması |
| `menu_goster()` | Ana menü çıktısı |
| `guvenli_tutar_al()` | Hatalı girişte tekrar sorar |
| `guvenli_tarih_al()` | Boş = bugün |

### `islem_yonetimi.py` – İşlem CRUD
| Fonksiyon | Açıklama |
|---|---|
| `gelir_ekle(yonetici)` | Doğrulanmış gelir kaydı ekler |
| `gider_ekle(yonetici)` | Doğrulanmış gider kaydı ekler |
| `islemleri_listele(yonetici)` | Renkli tablo & özet |
| `islem_sil(yonetici)` | ID ile silme + onay |

### `dosya_islemleri.py` – CSV
| Fonksiyon | Açıklama |
|---|---|
| `csv_kaydet(yonetici, dosya)` | Tüm işlemleri CSV'ye yazar; `aylik_ozet.csv`'yi de otomatik günceller |
| `csv_oku(yonetici, dosya)` | CSV'den yükleyip listeleri doldurur |

### `analiz.py` – Pandas & NumPy
| Fonksiyon | Açıklama |
|---|---|
| `verileri_dataframe_yap(yonetici)` | `pd.DataFrame` döndürür |
| `toplam_gelir_gider(df)` | Genel özet dict |
| `aylik_analiz(df)` | Aylık pivot tablo |
| `numpy_istatistik(df)` | Ort/Min/Max/Std/Medyan |

### `gorsellestirme.py` – Grafikler
| Fonksiyon | Açıklama |
|---|---|
| `aylik_grafik(df)` | Çizgi grafik → `grafikler/aylik_cizgi.png` |
| `gelir_gider_bar(df)` | Sütun grafik → `grafikler/gelir_gider_bar.png` |
| `pasta_grafik(df)` | Pasta grafik → `grafikler/pasta.png` |

### `excel_aktar.py` – Excel
Tek bir `.xlsx` dosyasına **3 sayfa** oluşturur:
1. **İşlemler** – Tüm kayıtlar, renk kodlu, net bakiye özeti
2. **Aylık Özet** – Kâr/Zarar sütunlu tablo (CSV gibi güncel)
3. **İstatistikler** – NumPy sonuçları

---

## 🗂 Kullanılan Veri Yapıları

```python
gelirler: list[Islem]   # FinansYoneticisi.gelirler
giderler: list[Islem]   # FinansYoneticisi.giderler
```

Her `Islem` nesnesi: `id (int)`, `tutar (float)`, `tarih (str YYYY-MM-DD)`,
`aciklama (str)`, `tip ('gelir' | 'gider')`

---

## 📋 Menü Yapısı

```
1  ➕  Gelir Ekle
2  ➖  Gider Ekle
3  📋  Listele
4  📊  Analiz Yap
5  📈  Grafik Göster
6  💾  CSV Kaydet / Yükle
7  📥  Excel'e Aktar
8  🗑   İşlem Sil
0  🚪  Çıkış
```

---

## ✅ Teknik Özellikler

- **OOP:** `Islem` sınıfı, `FinansYoneticisi` konteyner sınıfı
- **Modüler yapı:** Her sorumluluk ayrı `.py` dosyasında
- **Hata yönetimi:** `try-except` blokları ile kullanıcı girdileri ve dosya işlemleri korunur
- **Clean Code:** Docstring, anlamlı isimler, tek sorumluluk prensibi
- **CSV + Excel:** Hem `.csv` hem `.xlsx` desteklenir; aylık özet otomatik güncellenir
- **Grafikler:** Koyu tema, 150 DPI PNG çıktısı
