# Personalized Product Recommendation Engine

A hybrid recommendation system combining **collaborative filtering**, **content-based filtering**, and **explainable AI (SHAP)** for personalized product recommendations in e-commerce.

## 🎯 Key Features

- **Hybrid Filtering**: Combines user-item interactions (collaborative) with product features (content-based)
- **Deep Learning Models**: TensorFlow-based neural networks for recommendation scoring
- **SHAP Explanability**: Explains why each product was recommended to the user
- **Real-time Logging**: Continuous capture of user interactions for model refinement
- **Scalable Architecture**: MongoDB for flexible data storage, FastAPI for high-concurrency
- **Interactive UI**: Tailwind CSS-based responsive dashboard with recommendation cards

## 🏗️ Architecture

```
recommendation-engine/
├── core/                    # Configuration & security
│   ├── config.py
│   ├── dependencies.py
│   └── security.py
├── backend/
│   ├── api/                 # FastAPI endpoints
│   │   ├── users.py
│   │   ├── products.py
│   │   └── recommendations.py
│   └── models/              # Pydantic schemas
├── ml/
│   ├── hybrid_filtering/    # Recommendation algorithms
│   │   ├── collaborative.py
│   │   ├── content_based.py
│   │   └── hybrid.py
│   ├── explainability/      # SHAP integration
│   │   └── shap_explainer.py
│   └── preprocessing/       # Data preparation
│       └── preprocessor.py
├── db/                      # MongoDB interface
│   └── mongo.py
├── frontend/                # Web interface
│   ├── templates/           # HTML templates
│   └── static/              # CSS, JS, images
├── services/                # Business logic
│   └── recommendation_service.py
├── utils/                   # Utilities
├── tests/                   # Unit & integration tests
├── main.py                  # Application entry point
├── requirements.txt         # Python dependencies
├── Dockerfile               # Container configuration
├── docker-compose.yml       # Orchestration
└── README.md               # This file
```

## 📦 Technical Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Backend** | FastAPI + Python 3.10+ | High-performance async API |
| **ML Models** | TensorFlow + Keras | Deep learning for recommendations |
| **Explainability** | SHAP | Model interpretability |
| **Data Processing** | Pandas + NumPy + Scikit-Learn | Feature engineering |
| **Database** | MongoDB + Motor | Flexible document storage |
| **Frontend** | HTML5 + Tailwind CSS + JavaScript | Responsive UI |
| **Server** | Uvicorn | ASGI application server |
| **Proxy** | Nginx | Load balancing & static files |
| **Containerization** | Docker + Docker Compose | DevOps & deployment |

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose (recommended)
- Python 3.10+
- MongoDB 7.0+

### Local Setup

1. **Clone the repository**
   ```bash
   git clone <repo-url>
   cd recommendation-engine
   ```

2. **Create environment file**
   ```bash
   cp .env.example .env
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run with Docker Compose**
   ```bash
   docker-compose up -d
   ```

5. **Access the application**
   - Frontend: http://localhost
   - API: http://localhost/api
   - API Docs: http://localhost/api/docs (Swagger UI)

### Manual Setup (without Docker)

1. **Start MongoDB**
   ```bash
   mongod --version  # Verify installation
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application**
   ```bash
   python main.py
   ```

4. **Open browser**
   - http://localhost:8000

## 📚 API Endpoints

### Recommendations
- `POST /api/recommendations/` - Get personalized recommendations
- `POST /api/recommendations/{user_id}/feedback` - Log user interaction

### Products
- `GET /api/products/` - List all products
- `GET /api/products/{product_id}` - Get product details
- `POST /api/products/` - Create new product

### Users
- `GET /api/users/{user_id}` - Get user profile
- `POST /api/users/{user_id}/preferences` - Update preferences

### Health
- `GET /health` - Health check
- `GET /api/info` - API information

## 🤖 Hybrid Filtering Algorithm

The recommendation engine uses a weighted combination:

$$\text{Score} = 0.6 \times \text{Collaborative} + 0.4 \times \text{Content-Based}$$

**Collaborative Filtering**: Uses neural embeddings to find similar users and their preferences

**Content-Based Filtering**: Matches user preferences against product attributes

## 💡 SHAP Explainability

For each recommendation, SHAP calculates feature importance:

```
✓ Category Match: 80%
✓ Brand Match: 60%
✓ Price Range: 100%
✓ Product Rating: 90%
✓ User Engagement: 75%
```

## 📊 Data Models

### User
```json
{
  "_id": "user_123",
  "name": "John Doe",
  "email": "john@example.com",
  "preferences": {
    "categories": ["skincare", "organic"],
    "brands": ["brand_a", "brand_b"],
    "price_range": {"min": 10, "max": 100}
  }
}
```

### Product
```json
{
  "_id": "prod_456",
  "name": "Organic Skincare Serum",
  "category": "skincare",
  "brand": "brand_a",
  "price": 45.99,
  "rating": 4.8,
  "description": "Premium organic serum for sensitive skin",
  "tags": ["organic", "vegan", "cruelty-free"]
}
```

### Interaction
```json
{
  "_id": "int_789",
  "user_id": "user_123",
  "product_id": "prod_456",
  "interaction_type": "purchase",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## 🧪 Testing

```bash
# Run all tests
pytest

# Run specific test module
pytest tests/test_hybrid_filtering.py -v

# Run with coverage
pytest --cov=. --cov-report=html
```

## 📈 Performance Optimization

- **Caching**: Recommendations are cached for 1 hour
- **Batch Processing**: Processes user interactions in batches for efficiency
- **Database Indexing**: Optimized indexes on frequently queried fields
- **Gzip Compression**: Enabled for API responses
- **Async Operations**: Non-blocking database calls with Motor

## 🔒 Security

- JWT authentication for API endpoints
- Password hashing with bcrypt
- Environment-based configuration
- CORS protection
- Rate limiting (configurable)

## 📝 Configuration

Edit `.env` file to customize:

```env
# Server
DEBUG=False
HOST=0.0.0.0
PORT=8000

# Database
MONGODB_URL=mongodb://admin:password@mongodb:27017
DATABASE_NAME=recommendation_engine

# ML Settings
EMBEDDING_DIM=64
SHAP_ENABLED=True
TOP_FEATURES=5

# Logging
LOG_LEVEL=INFO
```

## 📖 Documentation

- **API Docs**: Swagger UI at `/api/docs`
- **OpenAPI Schema**: `/api/openapi.json`
- **Code Comments**: Comprehensive docstrings throughout

## 🛠️ Development

### Code Quality
```bash
# Format code
black .

# Lint
flake8 .

# Type checking
mypy .
```

### Adding New Features

1. Create feature branch: `git checkout -b feature/my-feature`
2. Implement with tests
3. Run quality checks
4. Submit pull request

## 📜 License

This project is part of the Capstone series and is for educational purposes.

## 🤝 Contributing

Contributions are welcome! Please follow:
- Code style: Black formatting
- Testing: Write unit tests for new features
- Documentation: Update README for major changes

## 📞 Support

For issues and questions:
- Check existing GitHub issues
- Create new issue with detailed description
- Contact development team

---

**Built with ❤️ for e-commerce excellence**
#   c a p s t o n e - P e r s o n a l i z e d - C l o t h i n g - R e c o m m e n d a t i o n - S y s t e m - f o r - E - C o m m e r c e  
 