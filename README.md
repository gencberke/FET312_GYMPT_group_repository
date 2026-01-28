# GYMPT - Görsel Besin Kalori Analizi ve Diyetisyen Yapay Zeka

> **FET312 Derin Öğrenme Dersi Grup Projesi**  
> İstanbul Topkapı Üniversitesi - 2024/2025 <br>
> [Proje sunum videosu linki](https://youtu.be/NrJmkyfn4Ho?si=525Gt_dv1v6iEnFe)

## 📋 Proje Özeti

GYMPT, yemek fotoğraflarından kalori ve besin değeri tahmini yapabilen, aynı zamanda kullanıcılarla Türkçe doğal dil ile iletişim kurabilen bir yapay zeka sistemidir. Proje, **görsel tanıma** ve **RAG tabanlı diyetisyen chatbot** olmak üzere iki ana modülden oluşmaktadır.

## 🏗️ Proje Mimarisi

```
┌─────────────────────────────────────────────────────────────────┐
│                         GYMPT Sistemi                           │
├─────────────────────────────┬───────────────────────────────────┤
│   🖼️ Görsel Analiz Modülü   │   💬 Diyetisyen Chatbot Modülü    │
│                             │                                   │
│  • Qwen2-VL (Fine-tuned)    │  • RAG (Retrieval Augmented Gen.) │
│  • Yemek Fotoğrafı Girişi   │  • ChromaDB Vector Store          │
│  • Kalori/Besin Tahmini     │  • Hybrid Search (BM25 + Vector)  │
│  • LoRA/QLoRA Adaptörleri   │  • TÜBER 2022 Bilgi Tabanı        │
└─────────────────────────────┴───────────────────────────────────┘
```

## 👥 Ekip Üyeleri ve Görevleri

| Öğrenci | Öğrenci No | Görev |
|---------|------------|-------|
| **Berke Genç** | 23040301058 | RAG Tabanlı Diyetisyen Chatbot (ChromaDB + Hybrid Search + Qwen2-VL) |
| **Hudaynazar Ishkabulov** | 22040101225 | Qwen2-VL Görsel Model Fine-tuning (LoRA) + Chatbot Eğitimi (Qwen2-7B) |
| **Halit Göymen** | 23040301091 | Qwen2-VL-7B LoRA Eğitimi (Chatbot + Vision) + Veri Hazırlama |
| **Emre Gürel** | 23040101047 | Neo4j Graf Veritabanı Entegrasyonu + Besin Veri İşleme |
| **Melih Erdem Koçoğlu** | 23040301064 | LangChain RAG Agent + Qwen2-VL Çoklu Yemek Analizi |
| **Muhammet Berat Arslan** | 23040101009 | Qwen2-VL-7B Görsel Besin Tespiti (Object Detection) |
| **Muhammet Yusuf Ünlü** | 23040301104 | Veri Seti Hazırlama (Parquet/JSON) + Qwen2-VL LoRA Eğitimi |
| **Naci İbrahim Ay** | 22040101051 | Veri Toplama (TÜBER PDF + FoodD + YOLO) + Unsloth Chatbot Eğitimi |

## 🛠️ Kullanılan Teknolojiler

### Derin Öğrenme & NLP
- **Qwen2-VL-2B/7B-Instruct** - Görsel-Dil Modeli (Vision-Language Model)
- **Qwen2.5-7B-Instruct** - Chatbot için LLM
- **intfloat/multilingual-e5-base** - Türkçe optimize embedding modeli
- **LoRA / QLoRA** - Parameter-Efficient Fine-Tuning
- **PEFT** - Hugging Face Parameter-Efficient Fine-Tuning
- **Unsloth** - Hızlı LLM fine-tuning
- **YOLO** - Nesne tespiti

### Vektör Veritabanı & Arama
- **ChromaDB** - Persistent vector storage
- **Neo4j** - Graf veritabanı (besin-kalori ilişkileri)
- **BM25Okapi** - Keyword-based search
- **RRF (Reciprocal Rank Fusion)** - Hybrid search fusion
- **LangChain** - RAG pipeline

### Veri İşleme
- **pdfplumber** - PDF metin çıkarma (TÜBER 2022)
- **Sentence-Transformers** - Text embedding
- **PyTorch** - Derin öğrenme framework'ü
- **FoodData Central** - USDA besin veritabanı

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
│   ├── Derin_proje_Gorsel_Eğitim.ipynb         # Qwen2-VL görsel model LoRA eğitimi
│   └── Derin_proje_ChatBot_Eğitim.ipynb        # Qwen2-7B chatbot LoRA eğitimi
│
├── HALİT_GÖYMEN_23040301091_GYMPT/
│   └── HALİT_GÖYMEN_23040301091_GYMPT.ipynb    # Qwen2-VL-7B LoRA (chatbot + vision)
│
├── EMRE_GÜREL_23040101047_GYMPT/
│   └── EMRE_GÜREL_23040101047_GYMPT.ipynb      # Neo4j graf DB + besin veri işleme
│
├── MELİH_ERDEM_KOCOGLU_23040301064_GYMPT/
│   └── MELİH_ERDEM_KOCOGLU_23040301064_GYMPT.ipynb  # LangChain RAG Agent
│
├── MUHAMMET_BERAT_ARSLAN_23040101009_GYMPT/
│   └── MUHAMMET_BERAT_ARSLAN_23040101009_GYMPT.ipynb # Qwen2-VL-7B görsel besin tespiti
│
├── MUHAMMET_YUSUF_ÜNLÜ_23040301104_GYMPT/
│   └── MUHAMMET_YUSUF_ÜNLÜ_23040301104_GYMPT.ipynb  # Veri hazırlama + LoRA eğitimi
│
├── NACİ_İBRAHİM_AY_22040101051_GYMPT/
│   └── NACİ_İBRAHİM_AY_22040101051_GYMPT.ipynb # Veri toplama + YOLO + Unsloth
│
├── SUNUM_VE_RAPOR_DOSYALARI/
│   ├── FET312_23040301058_GYMPT_ProjectOutline.pdf
│   ├── FET312_23040301091_GYMPT_ProjectReport.pdf
│   └── GYMPT-Gorsel-Besin-Kalori-Analizi-ve-Diyetisyen-Yapay-Zeka.pdf
│
└── README.md
```

## 🔧 Temel Bileşenler

### 1. RAG Diyetisyen Chatbot (Berke Genç)

TÜBER 2022 (Türkiye Beslenme Rehberi) dokümanını kullanarak beslenme sorularını yanıtlayan akıllı chatbot:

- **TextCleaner**: PDF'den çıkarılan bozuk Türkçe metinleri düzeltir
- **PDFProcessor**: Semantic chunking ile metni parçalara ayırır
- **ChromaVectorStore**: Embedding'leri ChromaDB'de saklar
- **HybridSearchEngine**: BM25 + Vector search kombinasyonu (RRF Fusion)
- **AnswerGenerator**: Qwen2-VL ile doğal dil yanıtı üretir

### 2. Görsel Besin Analizi

Yemek fotoğraflarından kalori ve besin değeri tahmini:

- **Qwen2-VL-2B/7B** base model
- **LoRA/QLoRA fine-tuning** ile özelleştirilmiş adaptörler
- **FoodD Dataset** + **Food Nutrients (Hugging Face)** ile eğitim
- Görsel + metin çoklu-modal girdi
- Çoklu yemek tespiti ve analizi

### 3. Graf Veritabanı Entegrasyonu (Emre Gürel)

- **Neo4j** ile besin-kalori-nutrient ilişkilerinin modellenmesi
- **FoodData Central** verilerinin graf yapısına dönüştürülmesi
- Qwen2-VL çıktılarının Neo4j sorguları ile zenginleştirilmesi

### 4. LangChain RAG Agent (Melih Erdem Koçoğlu)

- **FoodData Central JSON** veritabanı entegrasyonu
- **ChromaDB + HuggingFace Embeddings** ile vektör arama
- **Multi-food detection**: Tabaktaki tüm yemeklerin ayrı ayrı analizi
- İnteraktif diyetisyen sohbet modu

## 📊 Veri Kaynakları

1. **TÜBER 2022** - Türkiye Beslenme Rehberi (430 sayfa PDF)
2. **FoodD Dataset** - Yemek görselleri
3. **FoodData Central (USDA)** - Besin değerleri veritabanı
4. **mmathys/food-nutrients (HF)** - Hugging Face yemek veri seti
5. **Custom Q&A Dataset** - Beslenme soru-cevap çiftleri

## 🚀 Çalıştırma

### Gereksinimler
```bash
pip install transformers sentence-transformers rank_bm25 pdfplumber chromadb torch peft bitsandbytes accelerate qwen-vl-utils
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
- LoRA adaptörleri Hugging Face Hub veya Google Drive üzerinden yüklenebilir

## 📄 Lisans

Bu proje İstanbul Topkapı Üniversitesi FET312 Derin Öğrenme dersi kapsamında eğitim amaçlı geliştirilmiştir.

---

**İstanbul Topkapı Üniversitesi - Yazılım Mühendisliği Bölümü**  
*FET312 Derin Öğrenme - 2024/2025 Güz Dönemi*
