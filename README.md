# 🚀 Ollama Fine-Tuning Framework

A production-ready, end-to-end framework for fine-tuning and deploying custom language models using Ollama, with comprehensive monitoring, evaluation, and API serving capabilities.

---

## 📑 Quick Navigation

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Workflow](#-workflow)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [API Documentation](#-api-documentation)
- [Troubleshooting](#-troubleshooting)

---

## 🎯 Overview

### What is Ollama Fine-Tuning?

This framework enables you to take existing language models (like Mistral, Llama, etc.) and fine-tune them on your custom datasets to create specialized, domain-specific AI assistants.

### Why This Framework?

✅ **Easy to Use** - Simple CLI and web interface  
✅ **Production Ready** - Built for real-world deployment  
✅ **Scalable** - Supports distributed training  
✅ **Monitored** - Real-time training dashboard  
✅ **Safe** - No sensitive data in version control  

### Use Cases

- 📚 **Document Q&A** - Train models on your knowledge base
- 💼 **Customer Support** - Create specialized support chatbots
- 🔬 **Domain Experts** - Build models for specific industries
- 📝 **Code Generation** - Fine-tune for your coding style
- 🗣️ **Language Translation** - Customize for specific domains

---

## 🏗️ Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────────┐
│                   Ollama Fine-Tuning Platform                   │
└─────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   ┌─────────────┐      ┌──────────────┐      ┌─────────────┐
   │   DATA      │      │   TRAINING   │      │ EVALUATION  │
   │   LAYER     │      │   ENGINE     │      │  PIPELINE   │
   └────────────┬┘      └──────┬───────┘      └──────┬──────┘
                │              │                     │
                └──────────────┼─────────────────────┘
                               │
                        ┌──────▼────────┐
                        │  MODEL STORE  │
                        │  & VERSIONING │
                        └──────┬────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
   ┌─────────────┐      ┌────────────┐        ┌────────────┐
   │  OLLAMA     │      │  DASHBOARD │        │ REST API   │
   │  RUNTIME    │      │  (Gradio)  │        │  SERVER    │
   └─────────────┘      └────────────┘        └────────────┘
        │                     │                      │
        └─ Production ────────┼──────────── Inference ┘
                              │
                    ┌─────────▼──────────┐
                    │  MONITORING &      │
                    │  LOGGING SYSTEM    │
                    └────────────────────┘
```

### Component Breakdown

| Component | Purpose | Technology |
|-----------|---------|-----------|
| **Data Layer** | Ingests and preprocesses datasets | Python, Pandas, JSONL |
| **Training Engine** | Fine-tunes base models | PyTorch, Ollama, HuggingFace |
| **Evaluation** | Measures model quality | BLEU, ROUGE, Perplexity |
| **Model Store** | Version control & artifacts | Git LFS, Local Storage |
| **Dashboard** | Real-time monitoring UI | Gradio, Python |
| **API Server** | Production model serving | FastAPI/Flask, REST |
| **Runtime** | Model execution | Ollama |

---

## 🔄 Workflow

### Complete Training Pipeline

```
┌─────────────────────────────────────────────────────────────┐
│                  OLLAMA FINE-TUNING WORKFLOW                 │
└─────────────────────────────────────────────────────────────┘

PHASE 1: PREPARATION
  │
  ├─ 1.1 Data Collection
  │      └─ Gather raw datasets (CSV, TXT, JSON)
  │
  ├─ 1.2 Data Formatting
  │      └─ Convert to JSONL format: {"text": "...", "label": "..."}
  │
  ├─ 1.3 Data Validation
  │      └─ Check format, remove duplicates, validate structure
  │
  └─ 1.4 Data Splitting
         └─ Train (70%), Validation (15%), Test (15%)

                            ↓

PHASE 2: MODEL SETUP
  │
  ├─ 2.1 Choose Base Model
  │      └─ Options: Mistral, Llama 2, Neural Chat, etc.
  │
  ├─ 2.2 Download Weights
  │      └─ ollama pull mistral
  │
  ├─ 2.3 Configure Hyperparameters
  │      └─ Learning rate, batch size, epochs, etc.
  │
  └─ 2.4 Environment Setup
         └─ Install dependencies, allocate GPU memory

                            ↓

PHASE 3: FINE-TUNING
  │
  ├─ 3.1 Initialize Training
  │      └─ Load base model + training data
  │
  ├─ 3.2 Training Loop (Per Epoch)
  │      ├─ Forward pass through model
  │      ├─ Calculate loss
  │      ├─ Backward pass (gradient calculation)
  │      └─ Update model weights
  │
  ├─ 3.3 Monitoring
  │      ├─ Track loss metrics
  │      ├─ Log learning curves
  │      └─ Save checkpoints every N steps
  │
  └─ 3.4 Validation
         └─ Evaluate on validation set periodically

                            ↓

PHASE 4: EVALUATION
  │
  ├─ 4.1 Test Set Evaluation
  │      └─ Run comprehensive test suite
  │
  ├─ 4.2 Calculate Metrics
  │      ├─ BLEU Score (translation quality)
  │      ├─ ROUGE Score (summarization quality)
  │      ├─ Perplexity (language fluency)
  │      ├─ Accuracy (classification tasks)
  │      └─ Latency (inference speed)
  │
  ├─ 4.3 Compare with Baseline
  │      └─ Compare against original model
  │
  └─ 4.4 Generate Report
         └─ Create performance report

                            ↓

PHASE 5: DEPLOYMENT
  │
  ├─ 5.1 Package Model
  │      └─ Create model artifacts
  │
  ├─ 5.2 Version Control
  │      └─ Tag: model-v1.0-mistral-finetuned
  │
  ├─ 5.3 Push to Registry
  │      └─ Store in model registry/storage
  │
  ├─ 5.4 Deploy to Production
  │      └─ Run with Ollama service
  │
  └─ 5.5 Start API Server
         └─ Expose via REST API

                            ↓

PHASE 6: MONITORING
  │
  ├─ 6.1 Track Metrics
  │      ├─ Inference latency
  │      ├─ Resource usage (GPU, memory)
  │      └─ Request throughput
  │
  ├─ 6.2 Collect Feedback
  │      └─ User ratings and corrections
  │
  ├─ 6.3 Performance Alerts
  │      └─ Alert on degradation
  │
  └─ 6.4 Continuous Improvement
         └─ Plan next iteration
```

### Dashboard Interactive Workflow

```
╔════════════════════════════════════════════════════════════╗
║        Ollama Dashboard (Web Interface - Port 7860)        ║
╠════════════════════════════════════════════════════════════╣
║                                                              ║
║  ┌────────────────────────────────────────────────────┐   ║
║  │ 📋 CONFIGURATION SECTION                           │   ║
║  ├────────────────────────────────────────────────────┤   ║
║  │ • Select Base Model (Mistral, Llama, etc.)         │   ║
║  │ • Upload Dataset (CSV, JSONL)                      │   ║
║  │ • Set Hyperparameters:                             │   ║
║  │    - Learning Rate: 2e-5                           │   ║
║  │    - Batch Size: 8                                 │   ║
║  │    - Epochs: 10                                    │   ║
║  │    - Warmup Steps: 500                             │   ║
║  │ • Configure Training Schedule                      │   ║
║  └────────────────┬─────────────────────────────────┘   ║
║                   │ User clicks "START TRAINING"        ║
║  ┌────────────────▼─────────────────────────────────┐   ║
║  │ ⚙️  TRAINING PROGRESS MONITOR                     │   ║
║  ├────────────────────────────────────────────────────┤   ║
║  │ Epoch: 3/10 [████████░░░░░░░░░░░░░░░░░░░░░░ 30%]   │   ║
║  │ Batch: 45/100                                     │   ║
║  │ Loss: 0.3421 (↓ improving)                        │   ║
║  │ Learning Rate: 2e-5                               │   ║
║  │ GPU Memory: 8.2/24GB                              │   ║
║  │ ETA: 2h 15m remaining                             │   ║
║  │                                                     │   ║
║  │ 📈 Live Loss Curve                                │   ║
║  │    │                                               │   ║
║  │    ├─── Epoch 1: 2.104                            │   ║
║  │    ├─── Epoch 2: 1.203                            │   ║
║  │    └─── Epoch 3: 0.342 ← Current                  │   ║
║  └────────────────┬─────────────────────────────────┘   ║
║                   │ Training Complete                    ║
║  ┌────────────────▼─────────────────────────────────┐   ║
║  │ 🧪 EVALUATION & TESTING                          │   ║
║  ├────────────────────────────────────────────────────┤   ║
║  │ [Run Evaluation Pipeline]                         │   ║
║  │ [Compare with Baseline]                           │   ║
║  │ [Test with Custom Prompts]                        │   ║
║  │                                                     │   ║
║  │ Results:                                           │   ║
║  │ • BLEU Score: 0.82 (↑ +0.15 vs baseline)         │   ║
║  │ • ROUGE-1: 0.78                                   │   ║
║  │ • Perplexity: 45.2 (↓ lower is better)           │   ║
║  │ • Latency: 125ms per inference                    │   ║
║  └────────────────┬─────────────────────────────────┘   ║
║                   │ Evaluation Complete                  ║
║  ┌────────────────▼─────────────────────────────────┐   ║
║  │ 🚀 MODEL MANAGEMENT                              │   ║
║  ├────────────────────────────────────────────────────┤   ║
║  │ • Version: model-v1.0-mistral-finetuned          │   ║
║  │ • Status: ✅ Ready for Deployment                │   ║
║  │ • Size: 7.3GB                                     │   ║
║  │                                                     │   ║
║  │ Actions:                                           │   ║
║  │ [Download Model] [Deploy to Production]           │   ║
║  │ [View Model Card] [Compare Versions]              │   ║
║  │ [Export to Hugging Face] [Archive]                │   ║
║  └────────────────────────────────────────────────────┘   ║
║                                                              ║
╚════════════════════════════════════════════════════════════╝
```

---

## 📦 Installation

### Prerequisites

```
✓ Python 3.9 or higher
✓ 16GB RAM (32GB recommended)
✓ 50GB+ free storage
✓ CUDA 11.8+ (optional, for GPU acceleration)
✓ Ollama installed (https://ollama.ai)
```

### Step 1: Clone Repository

```bash
git clone https://github.com/Sakethkumar31/Fintech-ollama.git
cd Fintech-ollama
```

### Step 2: Create Virtual Environment

```bash
# Windows
python -m venv venv
.\venv\Scripts\Activate.ps1

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### Step 4: Setup Environment

```bash
# Copy example env file
cp .env.example .env

# Edit .env with your configuration
# Important: NEVER commit .env file to git
```

**Example .env:**
```env
OLLAMA_MODEL=mistral
OLLAMA_HOST=localhost:11434
TRAINING_EPOCHS=10
BATCH_SIZE=8
LEARNING_RATE=2e-5
DASHBOARD_PORT=7860
USE_GPU=true
```

---

## ⚡ Quick Start

### Option 1: Web Dashboard (Easiest)

```bash
# Windows
.\run_dashboard_web.bat

# macOS/Linux
bash run_dashboard_web.sh

# Manually
python gradio_app.py
```

Then open http://localhost:7860 in your browser.

### Option 2: Command Line

```bash
# 1. Download a base model
ollama pull mistral

# 2. Prepare your data
python scripts/prepare_dataset.py --input data/raw/tweets.csv --output data/processed/tweets.jsonl

# 3. Start training
python -c "
from fine_tune.trainer import ModelTrainer

trainer = ModelTrainer(
    model='mistral',
    dataset_path='data/processed/tweets.jsonl',
    output_dir='./models/finetuned'
)
trainer.train(epochs=5, batch_size=8)
"

# 4. Evaluate
python scripts/evaluate_model.py \
    --model ./models/finetuned/my_model \
    --test_data data/test/test.jsonl

# 5. Deploy API
python api/server.py --host 0.0.0.0 --port 8000
```

---

## ✨ Features

### 🎓 Training Features
- ✅ Support for multiple base models (Mistral, Llama, etc.)
- ✅ Distributed training with multiple GPUs
- ✅ Mixed precision training (FP16) for faster convergence
- ✅ Gradient accumulation for larger effective batch sizes
- ✅ Custom learning rate scheduling
- ✅ Checkpoint saving and resumption
- ✅ Early stopping based on validation metrics

### 📊 Evaluation Features
- ✅ Multiple metrics (BLEU, ROUGE, Perplexity, F1, Accuracy)
- ✅ Human-readable evaluation reports
- ✅ Model comparison (v1 vs v2)
- ✅ Benchmark suite with standard datasets
- ✅ Custom test set evaluation

### 🎨 UI Features
- ✅ Web dashboard with real-time monitoring
- ✅ Training progress visualization
- ✅ Loss curve plotting
- ✅ Interactive model testing
- ✅ Hyperparameter configuration UI
- ✅ One-click model deployment

### 🚀 Deployment Features
- ✅ REST API server with FastAPI
- ✅ Model versioning with Git
- ✅ Health checks and monitoring
- ✅ Rate limiting and authentication
- ✅ Batch inference support
- ✅ Model card generation

### 🔒 Security Features
- ✅ Environment variable protection (.env ignored)
- ✅ No sensitive data in version control
- ✅ Input validation and sanitization
- ✅ API authentication support
- ✅ Audit logging

---

## 📁 Project Structure

```
Fintech-ollama/
│
├── README.md                  # This file
├── SETUP_SUMMARY.md          # Setup verification
├── requirements.txt           # Python dependencies
├── .env.example              # Environment template
├── .gitignore               # Git exclusion rules
│
├── gradio_app.py            # Dashboard application
├── run_dashboard_web.bat    # Windows launcher
├── run_dashboard_web.sh     # Linux launcher
│
├── scripts/                 # Utility scripts
│   ├── setup_environment.py
│   ├── download_model.py
│   ├── prepare_dataset.py
│   ├── evaluate_model.py
│   └── compare_models.py
│
├── data/                    # Dataset directory
│   ├── raw/                 # Original data
│   ├── processed/           # Preprocessed data
│   ├── train/              # Training splits
│   ├── validation/         # Validation splits
│   └── test/               # Test splits
│
├── models/                  # Model storage
│   ├── base/               # Base models
│   ├── finetuned/          # Fine-tuned models
│   └── checkpoints/        # Training checkpoints
│
├── fine_tune/              # Training module
│   ├── trainer.py          # Main trainer
│   ├── optimizer.py        # Optimization utils
│   ├── callbacks.py        # Training callbacks
│   └── config.py           # Configuration
│
├── evaluation/             # Evaluation module
│   ├── metrics.py          # Metric functions
│   ├── benchmarks.py       # Benchmark suites
│   └── report_generator.py # Report generation
│
├── api/                    # API server
│   ├── server.py           # FastAPI app
│   ├── routes.py           # API endpoints
│   └── models.py           # Data models
│
├── utils/                  # Utility functions
│   ├── data_loader.py      # Data loading
│   ├── logger.py           # Logging setup
│   ├── validators.py       # Input validation
│   └── helpers.py          # Helper functions
│
└── logs/                   # Logs directory
    ├── training/
    ├── evaluation/
    └── server/
```

---

## 📡 API Documentation

### REST API Endpoints

#### 1. **Health Check**
```bash
GET /health

Response:
{
  "status": "healthy",
  "model": "mistral-finetuned-v1.0",
  "gpu_available": true,
  "memory_usage": 45.2
}
```

#### 2. **Generate Text**
```bash
POST /generate

Request:
{
  "prompt": "What is artificial intelligence?",
  "max_tokens": 200,
  "temperature": 0.7
}

Response:
{
  "generated_text": "Artificial intelligence refers to...",
  "tokens": 187,
  "latency_ms": 125
}
```

#### 3. **Batch Inference**
```bash
POST /batch_generate

Request:
{
  "prompts": [
    "Explain quantum computing",
    "What is deep learning?"
  ],
  "max_tokens": 150
}

Response:
{
  "results": [
    {"text": "Quantum computing uses...", "tokens": 142},
    {"text": "Deep learning is...", "tokens": 138}
  ],
  "total_latency_ms": 220
}
```

#### 4. **Model Info**
```bash
GET /model/info

Response:
{
  "name": "mistral-finetuned-v1.0",
  "version": "1.0",
  "size_gb": 7.3,
  "parameters": "7B",
  "created": "2026-04-22T10:30:00Z",
  "metrics": {
    "bleu": 0.82,
    "rouge_1": 0.78,
    "perplexity": 45.2
  }
}
```

---

## 🐛 Troubleshooting

### Issue: CUDA Out of Memory

**Solution:**
```env
BATCH_SIZE=4
GRADIENT_ACCUMULATION_STEPS=2
MAX_SEQ_LENGTH=1024
MIXED_PRECISION=fp16
```

### Issue: Ollama Connection Failed

**Solution:**
```bash
# Start Ollama service
ollama serve

# Verify connection
curl http://localhost:11434/api/tags
```

### Issue: Dashboard Not Loading

**Solution:**
```bash
# Check if port is in use
netstat -ano | findstr :7860

# Use different port
python gradio_app.py --server_port 7861
```

### Issue: Out of Storage

**Solution:**
```bash
# Check model size
ls -lah models/

# Clean up old checkpoints
rm -rf models/checkpoints/old_*

# Move data to larger drive
mv data/ /path/to/larger/drive/
```

---

## 📊 Performance Optimization

1. **Use Mixed Precision**: 50% faster training
2. **Gradient Accumulation**: Simulate larger batch sizes
3. **Data Caching**: Pre-load datasets in memory
4. **Distributed Training**: Use multiple GPUs
5. **Model Quantization**: Reduce inference latency

---

## 📝 Data Format

### JSONL Format (Recommended)

```jsonl
{"text": "Sample training text one", "category": "example"}
{"text": "Sample training text two", "category": "example"}
{"text": "Sample training text three", "category": "example"}
```

### CSV Format

```csv
text,category
"Sample training text one","example"
"Sample training text two","example"
```

---

## 🔐 Security Notes

✅ **Never commit:**
- `.env` files with secrets
- API keys or credentials
- Personal data
- Sensitive models

✅ **Always use:**
- Environment variables for secrets
- `.gitignore` for sensitive files
- HTTPS for API deployment
- Authentication for API endpoints

---

## 🤝 Contributing

```bash
# Create feature branch
git checkout -b feature/amazing-feature

# Make changes and test
pytest tests/

# Format code
black . && isort .

# Commit and push
git commit -m "Add amazing feature"
git push origin feature/amazing-feature
```

---

## 📚 Resources

- [Ollama Documentation](https://github.com/ollama/ollama)
- [HuggingFace Training Guide](https://huggingface.co/docs/transformers/training)
- [PyTorch Optimization](https://pytorch.org/docs/stable/optim.html)
- [Fine-tuning Best Practices](https://arxiv.org/abs/1911.02727)

---

## 📄 License

MIT License - See LICENSE file for details

