# GYMPT - Görsel Besin Kalori Analizi ve Diyetisyen Yapay Zeka

> **FET312 Derin Öğrenme Dersi Grup Projesi**  
> İstanbul Topkapı Üniversitesi - 2024/2025 <br>
> https://youtu.be/NrJmkyfn4Ho?si=525Gt_dv1v6iEnFe

## 📋 Proje Özeti

GYMPT, yemek fotoğraflarından kalori ve besin değeri tahmini yapabilen, aynı zamanda kullanıcılarla Türkçe doğal dil ile iletişim kurabilen bir yapay zeka sistemidir. Proje, **görsel tanıma** ve **RAG tabanlı diyetisyen chatbot** olmak üzere iki ana modülden oluşmaktadır.

## 🏗️ Proje Mimarisi

```
┌─────────────────────────────────────────────────────────────────┐
│                         GYMPT Sistemi                           │
├─────────────────────────────┬───────────────────────────────────┤
│   🖼️ Görsel Analiz Modülü   │   💬 Diyetisyen Chatbot Modülü    │
│                             │                                   │
│  • Qwen2-VL-2B (Fine-tuned) │  • RAG (Retrieval Augmented Gen.) │
│  • Yemek Fotoğrafı Girişi   │  • ChromaDB Vector Store          │
│  • Kalori/Besin Tahmini     │  • Hybrid Search (BM25 + Vector)  │
│  • LoRA/QLoRA Adaptörleri   │  • TÜBER 2022 Bilgi Tabanı        │
└─────────────────────────────┴───────────────────────────────────┘
```

## 👥 Ekip Üyeleri ve Görevleri

| Öğrenci | Öğrenci No | Görev |
|---------|------------|-------|
| **Berke Genç** | 23040301058 | RAG Tabanlı Diyetisyen Chatbot (ChromaDB + Hybrid Search) |
| **Hudaynazar Ishkabulov** | 22040101225 | Görsel Model Eğitimi + Chatbot Fine-tuning |
| **Halit Göymen** | 23040301091 | Qwen2-VL Görsel Model Fine-tuning (LoRA) |
| **Emre Gürel** | 23040101047 | Model Entegrasyonu ve Test |
| **Melih Erdem Koçoğlu** | 23040301064 | LangChain + ChromaDB Entegrasyonu |
| **Muhammet Berat Arslan** | 23040101009 | Veri Seti Hazırlama ve Preprocessing |
| **Muhammet Yusuf Ünlü** | 23040301104 | Model Değerlendirme ve Optimizasyon |
| **Naci İbrahim Ay** | 22040101051 | Veri Toplama (TÜBER + FoodD Dataset) |

## 🛠️ Kullanılan Teknolojiler

### Derin Öğrenme & NLP
- **Qwen2-VL-2B-Instruct** - Görsel-Dil Modeli (Vision-Language Model)
- **intfloat/multilingual-e5-base** - Türkçe optimize embedding modeli
- **LoRA / QLoRA** - Parameter-Efficient Fine-Tuning
- **PEFT (Parameter-Efficient Fine-Tuning)** - Hugging Face kütüphanesi

### Vektör Veritabanı & Arama
- **ChromaDB** - Persistent vector storage
- **BM25Okapi** - Keyword-based search (rank_bm25)
- **RRF (Reciprocal Rank Fusion)** - Hybrid search fusion algoritması

### Veri İşleme
- **pdfplumber** - PDF metin çıkarma
- **Sentence-Transformers** - Text embedding
- **PyTorch** - Derin öğrenme framework'ü

### Altyapı
- **Google Colab (A100 GPU)** - Model eğitimi
- **Hugging Face Hub** - Model paylaşımı
- **Google Drive** - Veri depolama

## 📁 Klasör Yapısı

```
FET312_GYMPT_group_repository/
│
├── BERKE_GENÇ_23040301058_GYMPT/
│   └── BERKE_GENÇ_23040301058_GYMPT.ipynb      # RAG Diyetisyen Chatbot
│
├── HUDAYNAZAR_ISHKABULOV_22040101225_GYMPT/
│   ├── Derin_proje_Gorsel_Eğitim.ipynb         # Görsel model fine-tuning
│   └── Derin_proje_ChatBot_Eğitim.ipynb        # Chatbot fine-tuning
│
├── HALİT_GÖYMEN_23040301091_GYMPT/
│   └── HALİT_GÖYMEN_23040301091_GYMPT.ipynb    # Qwen2-VL LoRA eğitimi
│
├── EMRE_GÜREL_23040101047_GYMPT/
│   └── EMRE_GÜREL_23040101047_GYMPT.ipynb      # Model entegrasyonu
│
├── MELİH_ERDEM_KOCOGLU_23040301064_GYMPT/
│   └── MELİH_ERDEM_KOCOGLU_23040301064_GYMPT.ipynb  # LangChain entegrasyonu
│
├── MUHAMMET_BERAT_ARSLAN_23040101009_GYMPT/
│   └── MUHAMMET_BERAT_ARSLAN_23040101009_GYMPT.ipynb # Veri preprocessing
│
├── MUHAMMET_YUSUF_ÜNLÜ_23040301104_GYMPT/
│   └── MUHAMMET_YUSUF_ÜNLÜ_23040301104_GYMPT.ipynb  # Model değerlendirme
│
├── NACİ_İBRAHİM_AY_22040101051_GYMPT/
│   └── NACİ_İBRAHİM_AY_22040101051_GYMPT.ipynb # Veri toplama
│
├── SUNUM_VE_RAPOR_DOSYALARI/
│   ├── FET312_23040301058_GYMPT_ProjectOutline.pdf
│   ├── FET312_23040301091_GYMPT_ProjectReport.pdf
│   └── GYMPT-Gorsel-Besin-Kalori-Analizi-ve-Diyetisyen-Yapay-Zeka.pdf
│
└── README.md
```

## 🔧 Temel Bileşenler

### 1. RAG Diyetisyen Chatbot 

TÜBER 2022 (Türkiye Beslenme Rehberi) dokümanını kullanarak beslenme sorularını yanıtlayan akıllı chatbot:

- **TextCleaner**: PDF'den çıkarılan bozuk Türkçe metinleri düzeltir
- **PDFProcessor**: Semantic chunking ile metni parçalara ayırır
- **ChromaVectorStore**: Embedding'leri ChromaDB'de saklar
- **HybridSearchEngine**: BM25 + Vector search kombinasyonu
- **AnswerGenerator**: Qwen2-VL ile doğal dil yanıtı üretir

### 2. Görsel Besin Tanıma 

Yemek fotoğraflarından kalori ve besin değeri tahmini:

- **Qwen2-VL-2B** base model
- **LoRA fine-tuning** ile özelleştirilmiş adaptörler
- **FoodD Dataset** ile eğitim
- Görsel + metin çoklu-modal girdi

## 📊 Veri Kaynakları

1. **TÜBER 2022** - Türkiye Beslenme Rehberi (430 sayfa PDF)
2. **FoodD Dataset** - Yemek görselleri ve besin değerleri
3. **Custom Q&A Dataset** - Beslenme soru-cevap çiftleri (3260+ örnek)

## 🚀 Çalıştırma

### Gereksinimler
```bash
pip install transformers sentence-transformers rank_bm25 pdfplumber chromadb torch peft bitsandbytes accelerate
```

### RAG Chatbot Kullanımı
```python
# Botu başlat
bot = DiyetisyenBot(CONFIG, force_reindex=True)

# Soru sor
answer, sources = bot.ask("Günde kaç kalori almalıyım?", return_sources=True)
print(answer)
```

## 📝 Notlar

- Model eğitimleri **Google Colab A100 GPU** üzerinde gerçekleştirilmiştir
- ChromaDB veritabanı lokal olarak `data_resources/chroma_db` klasöründe saklanır
- İlk çalıştırmada `force_reindex=True` ile PDF'in yeniden işlenmesi gerekir

## 📄 Lisans

Bu proje İstanbul Topkapı Üniversitesi FET312 Derin Öğrenme dersi kapsamında eğitim amaçlı geliştirilmiştir.

---

**İstanbul Topkapı Üniversitesi - Yazılım Mühendisliği Bölümü**  
*FET312 Derin Öğrenme - 2024/2025 Güz Dönemi*
