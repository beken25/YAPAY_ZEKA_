Şarkı Sözleri Metin Benzerliği Projesi

Bu proje, Gümüşhane Üniversitesi Yapay Zeka dersi kapsamında, şarkı sözü benzeri metinler üzerinde TF-IDF ve Word2Vec yöntemleriyle metin benzerliği hesaplamayı ve bu modelleri karşılaştırmalı olarak analiz etmeyi amaçlamaktadır. Çalışma, veri ön işleme, vektörleştirme, benzerlik hesaplama ve değerlendirme aşamalarını içermektedir.

---

 Projenin Amacı

* TF-IDF ve Word2Vec yöntemlerini kullanarak şarkı sözü benzeri metinler arasında benzerlik analizi yapmak.
* Elde edilen sonuçları Cosine Similarity ve Jaccard benzerliği ile değerlendirmek.
* Farklı model yapılandırmalarının (CBOW/SkipGram, pencere boyutu, vektör boyutu) çıktılara etkisini incelemek.

---

 Kullanılan Veri Seti

* **veri\_seti\_50mb.csv** dosyası, yaklaşık 50 MB büyüklüğünde, şarkı sözlerine benzer şekilde yapay olarak üretilmiş tematik metinler içermektedir.
* Gerçek veri çekme girişimleri Genius API ve Selenium yöntemleriyle denenmiş, ancak teknik kısıtlamalar nedeniyle bu veri yapay olarak oluşturulmuştur.

---

 Kurulum Talimatları

Gerekli Python kütüphaneleri:

```bash
pip install pandas numpy nltk gensim scikit-learn matplotlib
```

NLTK veri setlerini indirmeniz gerekebilir:

```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```

---

Kullanılan Yöntemler

### 1. Veri Ön İşleme

* Küçük harfe çevirme
* Noktalama temizliği
* Tokenization (nltk)
* Stopword temizleme
* Lemmatizasyon (zeyrek)
* Stemming

Her işlem sonucunda ayrı veri sütunları oluşturulmuştur.

### 2. Zipf Yasası Analizi

* Ham veri, lemmatize edilmiş ve stemmed veri için ayrı ayrı Zipf grafikleri çizilmiştir.
* Grafikler log-log eksende sunulmuş ve dağılımlar yorumlanmıştır.

### 3. Vektörleştirme

* **TF-IDF**: Hem lemmatized hem stemmed veriler için uygulanmış ve `tfidf_lemmatized.csv`, `tfidf_stemmed.csv` dosyaları oluşturulmuştur.
* **Word2Vec**: 8 farklı parametre kombinasyonuyla (CBOW/SkipGram, window=2/4, dim=100/300) toplam 16 model eğitilmiştir. Her biri için:

  * Model dosyası `.model` olarak kaydedilmiştir.
  * Örnek kelimeler için en yakın 5 kelime analiz edilmiştir.

### 4. Benzerlik Hesaplama

* Giriş metni: Veri setinden seçilen bir satır.
* Her model için giriş metnine en benzer ilk 5 metin Cosine Similarity ile hesaplanmıştır.
* Modellerin çıktıları görsel tablolarla karşılaştırılmıştır.

### 5. Değerlendirme

* **Anlamsal Değerlendirme**: Her model için çıkan ilk 5 sonuç, 1–5 arası puanlanmış ve ortalama skorlar elde edilmiştir.
* **Jaccard Benzerliği**: Tüm modellerin ilk 5 sonucu karşılaştırılarak 18x18'lik Jaccard matrisi oluşturulmuştur.

---

 Çıktı Dosyaları

* `tfidf_lemmatized.csv`, `tfidf_stemmed.csv`
* `word2vec_lemmatized_*`, `word2vec_stemmed_*` model dosyaları
* `benzerlik_karsilastirma_tablosu.csv`
* `jaccard_benzerlik_matrisi.csv`

---

 Yorumlar ve Sonuçlar

* Word2Vec modelleri, TF-IDF'e kıyasla daha yüksek benzerlik skorları üretmiştir.
* SkipGram modelleri genellikle CBOW'a göre daha tutarlı sonuçlar vermiştir.
* Jaccard benzerliği düşük olan modeller, anlamsal olarak da uzak sonuçlar üretmiştir.

---

 Hazırlayan

**Yusuf Beken**
Gümüşhane Üniversitesi – Yapay Zeka Dersi – 2025 Bütünleme Projesi
