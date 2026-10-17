# 🏋️‍♂️ FormaFit AI Assistant: RAG & Agentic LLM System

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-Models-orange)
![LangChain](https://img.shields.io/badge/LangChain-Integration-green)
![FAISS](https://img.shields.io/badge/FAISS-Vector_DB-lightgrey)
![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)

FormaFit AI Assistant, spor kulübü üyelerinin sorularını yanıtlamak, kuralları açıklamak ve dinamik hesaplamalar yapmak üzere geliştirilmiş, **Retrieval-Augmented Generation (RAG)** ve **Tool-Calling (Ajan)** yeteneklerine sahip ince ayarlı (fine-tuned) bir Büyük Dil Modeli projesidir.

## 🚀 Projenin Amacı ve Kapsamı

Bu proje, açık kaynaklı küçük boyutlu bir dil modelinin (1.5B parametre) kurumsal bir kimlik kazanması ve halüsinasyonları en aza indirerek dış kaynaklardan veri çekebilmesi amacıyla tasarlanmıştır. Model, yalnızca metin üretmekle kalmaz; aynı zamanda vektör veritabanından bağlam okuyabilir ve matematiksel hesaplamalar için dış Python fonksiyonlarını tetikleyebilir.

## ✨ Temel Özellikler

- **Özelleştirilmiş Kimlik (QLoRA Fine-Tuning):** Modelin ağırlıkları, "FitAsistan" kimliğini benimsemesi, kurumsal bir dil kullanması ve 🏋️‍♂️ emojisiyle yanıt vermesi için özel bir veri setiyle (sentetik JSONL) güncellenmiştir.
- **Bağlama Duyarlı Yanıtlar (RAG):** Kurum rehberindeki bilgiler parçalara ayrılarak (chunking) çok dilli `mpnet` embedding modeliyle sayısallaştırılmış ve **FAISS** vektör veritabanında indekslenmiştir. Kosinüs uzaklığı (cosine similarity) kullanılarak sorulara en alakalı bağlam getirilmektedir.
- **Dinamik Araç Kullanımı (Agentic Tool-Calling):** Model, statik cevaplar vermek yerine kullanıcı niyetini anlar ve gerektiğinde `pt_ucreti_hesapla()` gibi dış araçları (tools) doğru argümanlarla çağırarak matematiksel operasyonlar gerçekleştirir.
- **GGUF Dönüşümü & CPU Optimizasyonu:** Eğitim sonrası model `llama.cpp` ile 8-bit kuantize edilerek (q8_0) GGUF formatına dönüştürülmüş, böylece pahalı GPU gereksinimleri olmadan standart sunucularda (CPU) çalışabilir hale getirilmiştir.

## 🏗️ Mimari ve Teknoloji Yığını

- **Taban Model:** `Qwen/Qwen2.5-1.5B-Instruct`
- **Eğitim Yöntemi:** SFTTrainer ile QLoRA (r=16, alpha=32)
- **Vektör Veritabanı:** FAISS (Facebook AI Similarity Search)
- **Embedding Modeli:** `paraphrase-multilingual-mpnet-base-v2`
- **Arayüz:** Gradio / Streamlit

## ⚙️ Kurulum ve Çalıştırma

Güvenlik prensipleri gereği API anahtarları kaynak kodda bulunmaz. Projeyi lokalinizde çalıştırmak için aşağıdaki adımları izleyin:

1.  **Depoyu Klonlayın:**

    ```bash
    git clone [https://github.com/kullaniciadiniz/FormaFit-AI-Assistant.git](https://github.com/kullaniciadiniz/FormaFit-AI-Assistant.git)
    cd FormaFit-AI-Assistant
    ```

2.  **Gerekli Kütüphaneleri Yükleyin:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Çevre Değişkenlerini Ayarlayın:**
    Depoda bulunan `.env.example` dosyasının adını `.env` olarak değiştirin ve içine kendi ücretsiz API anahtarınızı ekleyin:

    ```env
    HUGGINGFACE_TOKEN=sizin_hf_tokeniniz_buraya
    ```

4.  **Uygulamayı Başlatın:**
    ```bash
    python app.py
    ```

## 📊 Performans ve Metrikler

- Gözetimli ince ayar (Supervised Fine-Tuning) 3 epoch boyunca yapılmıştır.
- Araç kullanımı testlerinde (örneğin Özel Ders maliyeti hesaplama) tek adımlı senaryolarda yüksek başarı gözlemlenmiştir.
- Detaylı değerlendirme metrikleri ve test sonuçları için Hugging Face Model Kartı incelenebilir.

## 🔗 Bağlantılar

- **Model Kartı (Hugging Face):** (https://huggingface.co/beyzakulac/FormaFit-Asistan-3B)]
- **GGUF Deposu:** https://huggingface.co/beyzakulac/FormaFit-Asistan-3B-GGUF
- **Eğitim Veri Seti:** (https://huggingface.co/beyzakulac/FormaFit-Asistan-3B)

---

_Bu proje, yapay zeka mühendisliği becerilerini geliştirmek ve RAG/Ajan mimarilerini test etmek amacıyla kurgusal verilerle oluşturulmuştur._
