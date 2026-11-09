# 🍽️ ML-Powered Restaurant Recommendation System

<div align="center">

![CI/CD Status](https://github.com/iamayushsaxena/ML-Restaurant-Recommendations/actions/workflows/ci.yml/badge.svg)
[![Python](https://img.shields.io/badge/Python-3.13+-blue.svg)](https://www.python.org/downloads/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.31+-red.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
![Status](https://img.shields.io/badge/Status-Portfolio%20Project-orange.svg)
![Maintenance](https://img.shields.io/badge/Maintained-Yes-brightgreen.svg)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-orange.svg)

![Banner Image](outputs/figures/banner.png)

**An end-to-end machine learning recommendation system designed to reduce decision fatigue on food delivery platforms by 40%**

**💻[Live Demo](https://ayush-saxena-ml-restaurant-recommendations.streamlit.app)** | **📓 [Documentation](https://github.com/iamayushsaxena/ML-Restaurant-Recommendations/tree/main/docs)** | **📝 [Full PRD](prd/restaurant_recommendations_prd.md)** | **🐞 [Report Bug](https://github.com/iamayushsaxena/ML-Restaurant-Recommendations/issues)**

<!-- Live Demo Badge -->
▶️ **Try the Live Demo:** [![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://ayush-saxena-ml-restaurant-recommendations.streamlit.app)

</div>

---

## 📸 Project Demo

<div align="center">

### Personalized Recommendations with Explanations

<img src="https://raw.githubusercontent.com/iamayushsaxena/ML-Restaurant-Recommendations/main/outputs/figures/demo-screenshot.png" alt="Demo Screenshot" width="800"/>

### Interactive Dashboard

<img src="https://raw.githubusercontent.com/iamayushsaxena/ML-Restaurant-Recommendations/main/outputs/figures/dashboard-screenshot.png" alt="Dashboard" width="800"/>

### Cold Start Onboarding Flow

<img src="https://raw.githubusercontent.com/iamayushsaxena/ML-Restaurant-Recommendations/main/outputs/figures/cold-start-screenshot.png" alt="Cold Start" width="800"/>

</div>

---

## 📋 Project Overview

### Problem Statement

Food delivery users face significant friction in the ordering process due to overwhelming restaurant choices and lack of contextual prioritization. This increases:

- **⏱️ Decision Fatigue**: Users spend 8-12 minutes browsing 200+ restaurant options and get overwhelmed
- **🛒 Cart Abandonment**: ~30% of users add items but don't complete checkout
- **🔄 Low Discovery**: 65% of orders are repeat orders from the same 3-5 restaurants
- **💸 Revenue Loss**: High-quality restaurants with availability go undiscovered

**Root Cause:** Current "Sort by: Distance/Rating/Delivery Time" approach is too generic and doesn't consider:
- User's historical preferences (cuisine, price, dietary needs)
- Contextual factors (time of day, weather, occasion)
- Real-time constraints (restaurant availability, delivery capacity)

---

### ✨ Solution Overview

An **ML-powered hybrid recommendation system** specifically for the **home feed** that combines:

### 1. Collaborative Filtering (40% weight)
- Learns from similar users' preferences
- "Users like you ordered from these restaurants"
- Enables discovery of unexpected matches

### 2. Content-Based Filtering (35% weight)
- Matches restaurant attributes to user profile
- Considers cuisine, price, rating, dietary restrictions
- Works even for new users (cold start handling)

### 3. Contextual Factors (25% weight)
- **Time of Day**: Breakfast → South Indian/Cafe, Dinner → Biryani/Chinese
- **Weather**: Rainy → Comfort food, Hot → Beverages/Desserts
- **Distance**: Exponential decay penalty for far restaurants
- **Popularity**: Slight boost for trending restaurants

**Hybrid Score Calculation:**
```python
Final Score = 0.40 × CF_Score + 0.35 × CB_Score + 0.25 × Context_Score
```

---

### ⭐ Success Metrics

**Primary Metric (Hero Metric):**
- **Time to Order**: Reduce by 40% (10 minutes → 6 minutes)

**Secondary Metrics:**
- Order conversion rate: +15% improvement
- Restaurant discovery: 2+ new restaurants per user per month
- Repeat order rate: Decrease from 65% to 55%

**Guardrail Metrics:**
- Average delivery time: ≤38 minutes
- Order cancellation rate: ≤6%
- User dissatisfaction: ≤10%

---

## 🚀 Key Features

<table>
<tr>
<td width="50%">

### 🎯 Personalized Recommendations
- Top-10 tailored to each user
- Context-aware (time, weather, location)
- Excludes closed restaurants
- <2 second response time

### 🧊 Cold Start Handling
- 3-question onboarding (<30 seconds)
- Content-based fallback strategy
- Works from first order

### 💡 Explainable AI
- Clear reason for each recommendation
- Examples: "You've ordered South Indian 3 times"
- Builds trust before ordering

</td>
<td width="50%">

### 🎨 Diversity Constraints
- Max 3 restaurants per cuisine
- Prevents filter bubble
- Balances familiarity (40%) with discovery (60%)

### 📊 Comprehensive Evaluation
- Precision@K, Recall@K, Hit Rate, NDCG
- Discovery metrics (diversity, novelty, coverage)
- Temporal train-test split

### 🔧 Production-Ready
- Fallback strategies for failures
- Edge case handling
- Complete documentation

</td>
</tr>
</table>

---

## 📁 Project Structure
```
ml-restaurant-recommendations/
│
├── data/                                   # All datasets
│   ├── synthetic/                          # Generated data
│   │   ├── users.csv                       # 50K users
│   │   ├── restaurants.csv                 # 500 restaurants
│   │   └── orders.csv                      # 200K orders
│   └── processed/                          # Engineered features
│       ├── user_features.csv
│       ├── restaurant_features.csv
│       └── interaction_matrix.csv
│
├── src/                                    # Source code
│   ├── config.py                           # Configuration
│   ├── data_generator.py                   # Synthetic data creation
│   ├── feature_engineering.py              # Feature engineering
│   ├── collaborative_filtering.py          # CF model
│   ├── content_based_filtering.py          # CBF model
│   ├── hybrid_recommender.py               # Hybrid system
│   ├── explainability.py                   # Explanation engine
│   ├── cold_start_handler.py               # New user handling
│   └── evaluation.py                       # Model evaluation
│
├── app/                                    # Streamlit application
│   └── streamlit_app.py                    # Interactive demo
│
├── models/                                 # Saved models
│   ├── collaborative_model.pkl
│   ├── content_based_model.pkl
│   └── hybrid_model.pkl
│
├── prd/                                    # Product documentation
│   ├── ab_test_plan.md                     # A/B testing strategy
│   ├── edge_cases.md                       # Handling edge cases
│   └── restaurant_recommendations_prd.md   # Full PRD
│
├── scripts/                                # Utility scripts
│   └── train_models.py                     # Master training script
│
├── tests/                                  # Unit tests
│   ├── test_recommender.py
│   ├── test_cold_start.py
│   └── test_explainability.py
│
├── docs/                                   # Technical documentation
│    ├── architecture.md                    # System design and data flow
│    ├── methodology.md                     # ML approach and evaluation
│    └── lab_logbook.md                     # Development log
│
├── .gitignore                              # Git ignore patterns
├── requirements.txt                        # Dependencies
├── LICENSE                                 # MIT License
└── README.md                               # This file
```

---

## ⚡ Quick Start

### Prerequisites
- Python 3.13 or higher
- pip package manager
- 4GB RAM minimum
- 500MB disk space

### Installation

**Step 1: Clone the repository**
```bash
git clone https://github.com/iamayushsaxena/ML-Restaurant-Recommendations.git
cd ml-restaurant-recommendations
```

**Step 2: Setup environment**
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
source venv/bin/activate           # On MacOS
                                      # OR
venv\Scripts\activate              # On Windows
```

**Step 3: Install dependencies**
```bash
pip install -r requirements.txt
```

**Step 4: Generate Data & Train Models**
```bash
# Run the master training script to generate data and train all models
python scripts/train_models.py
```
This will:
1. Generate synthetic dataset (50K users, 500 restaurants, 200K orders)
2. Engineer features for users and restaurants
3. Train collaborative filtering model
4. Train content-based filtering model
5. Create hybrid recommendation system

**Expected runtime:** ~3-5 minutes

**Step 5: Running the Demo**
```bash
# Launch the interactive Streamlit application
streamlit run app/streamlit_app.py
```

The app will open in your browser at `http://localhost:8501`

---

## 🎮 Demo

### 🌐 Live Demo
👉 **[Try the Interactive Demo on Streamlit Cloud](https://ayush-saxena-ml-restaurant-recommendations.streamlit.app)**

---

## 🔬 Technical Approach

### Model Architecture
```
User Request
    ↓
Extract Context (time, location, weather)
    ↓
    ├─────────────┬─────────────┬─────────────┐
    │             │             │             │
    ▼             ▼             ▼             ▼
Collaborative  Content-Based  Contextual   Business
Filtering      Filtering      Scoring      Rules
(40%)          (35%)          (25%)        
    │             │             │             │
    └─────────────┴─────────────┴─────────────┘
                    ↓
            Hybrid Ranker
                    ↓
        Apply Filters & Diversity
                    ↓
        Generate Explanations
                    ↓
        Return Top-N Recommendations
```

### Algorithms Used

**Collaborative Filtering:**
- User-based CF with cosine similarity
- Top-30 similar users for recommendation
- Handles sparsity with sparse matrix representation

**Content-Based Filtering:**
- Weighted feature matching (cuisine 40%, price 25%, rating 20%, delivery 15%)
- StandardScaler normalization
- Dietary restriction hard filters

**Contextual Scoring:**
- Time-based cuisine boosting (1.3-1.5× multiplier)
- Weather-based adjustments
- Distance decay (exponential: e^(-dist/3km))

**Hybrid Combination:**
```python
if user_order_count >= 3:
    final_score = 0.40*cf + 0.35*cb + 0.25*context
else:  # Cold start
    final_score = 0.75*cb + 0.25*context
```

---

## 📊 Evaluation Results

Evaluated on 100 test users with temporal train-test split:

### Accuracy Metrics

| Metric | @5 | @10 | @20 | Interpretation |
|--------|-----|-----|-----|----------------|
| **Precision** | 0.0842 | 0.0756 | 0.0621 | 7.6% of top-10 were ordered |
| **Recall** | 0.1234 | 0.2145 | 0.3521 | 21.5% of actual orders in top-10 |
| **Hit Rate** | 0.3156 | 0.4823 | 0.6421 | **48.2% users ordered from top-10** |
| **NDCG** | 0.2134 | 0.2567 | - | Good ranking quality |

### Discovery Metrics

| Metric | Score | Interpretation |
|--------|-------|----------------|
| **Diversity** | 0.7234 | 7+ cuisines in top-10 recommendations |
| **Novelty** | 0.6421 | 64% are new restaurants for user |
| **Coverage** | 0.4523 | 45% of catalog recommended across all users |

### Baseline Comparison

| Approach | Hit Rate@10 | Diversity | Trade-off Decision |
|----------|-------------|-----------|-------------------|
| Random | 0.05 | 0.85 | ❌ Too low accuracy |
| Popular Only | 0.32 | 0.23 | ❌ No personalization |
| Pure CF | 0.51 | 0.58 | ⚠️ Better accuracy but lower diversity |
| **Hybrid (Ours)** | **0.48** | **0.72** | ✅ **Best balance** |

**Decision Rationale:** Traded 3% hit rate for 24% more diversity to prevent recommendation fatigue.

---

## 💡 Product Thinking

### Key Design Decisions

#### 1. Time-to-Order over CTR
❌ **Could have optimized for:** Click-through rate (common ML metric)  
✅ **Chose instead:** Time-to-order  

**Why:** CTR is a vanity metric. It doesn't address the user's real pain: decision fatigue. Time-to-order directly measures whether we're solving the problem.

**PM Perspective:**
> "I could have optimized for CTR—that's what most ML projects do. But CTR doesn't address the user's pain point. A user clicking through 50 restaurants still takes 10 minutes to order. Time-to-order measures what actually matters: are we reducing decision fatigue?"

#### 2. Explainability over Pure Accuracy
❌ **Could have used:** Deep learning (2-3% better accuracy)  
✅ **Chose instead:** Simple models with clear explanations  

**Why:** Food recommendations require trust. Users won't order from a restaurant they don't understand why it was suggested. Explainability isn't optional—it's core to adoption.

**PM Perspective:**
> "I deliberately chose simpler models over deep learning. Why? Because food needs trust. Users won't order from a 'black box' recommendation. Every suggestion has a clear reason: 'You've ordered South Indian 3 times, rated 4.5/5 by 856 customers.' That's worth more than 2% accuracy."

#### 3. Diversity Constraints over Pure Precision
❌ **Could have shown:** Top-10 all from user's favorite cuisine  
✅ **Chose instead:** Max 3 restaurants per cuisine  

**Why:** Pure precision creates a filter bubble. Long-term user satisfaction requires variety. Prevent recommendation fatigue.

**PM Perspective:**
> "I enforce a max of 3 restaurants per cuisine in the top-10. This costs some precision but prevents the filter bubble. If I only showed North Indian because that's what you ordered before, you'd get bored fast. Discovery matters for retention."

### Success Metrics Framework

**Primary Metric (North Star):**
- **Time to Order**: 40% reduction (10 min → 6 min)
- **Why Primary:** Directly addresses user pain point

**Secondary Metrics:**
- Order conversion rate: +15%
- Restaurant discovery: 2+ new restaurants/month
- **Why Secondary:** Important but not the core problem

**Guardrail Metrics:**
- Average delivery time: ≤38 minutes
- Order cancellation rate: ≤6%
- User dissatisfaction: ≤10%
- **Why Guardrails:** Prevent quality degradation while optimizing primary metric

**Stakeholder Balance:**
- **Users**: Want relevance + variety (conflicting!)
- **Restaurants**: Want visibility (but fair distribution)
- **Platform**: Wants revenue (but not at cost of trust)

**Trade-offs Made:**
1. **Explainability > Accuracy**: Users need reasons before ordering food
2. **Diversity > Precision**: Prevent recommendation fatigue
3. **Speed > Perfection**: 6-minute decision time is "good enough"

---

## 📚 Documentation

### Product Documentation
- **[Complete PRD](prd/restaurant_recommendations_prd.md)** - Full product requirements document
- **[A/B Test Plan](prd/ab_test_plan.md)** - Statistical testing methodology
- **[Edge Cases](prd/edge_cases.md)** - Error handling and fallback strategies

### Technical Documentation
- **[Methodology](docs/methodology.md)** - ML approach, feature engineering, evaluation
- **[Architecture](docs/architecture.md)** - System design and data flow
- **[Lab Logbook](docs/lab_logbook.md)** - Step-by-step development process

---

## 🧪 Testing

Run unit tests:
```bash
# Install pytest
pip install pytest pytest-cov

# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ --cov=src --cov-report=html

# Run specific test file
pytest tests/test_recommender.py -v
```

---

## 🔮 Future Enhancements

### Out of Scope (V1) - Noted in PRD
- ❌ Dynamic pricing optimization
- ❌ Restaurant commission strategies  
- ❌ Courier assignment logic
- ❌ Long-term personalization (cross-month)
- ❌ Multi-city rollout strategy

### Potential V2 Features
- Real-time availability filtering
- Group ordering recommendations
- Dietary restriction hard filters (allergies)
- A/B test framework implementation
- Multi-armed bandit for exploration

---

## 🤝 Contributing

Contributions are welcome! This is a portfolio project, but I'm happy to accept improvements.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**TL;DR:** You can freely use, modify, and distribute this project, even commercially, as long as you include the original license.

---

## 📞 Contact & Connect

**👤Author:** Ayush Saxena

- 🔗 **LinkedIn:** [Ayush Saxena](https://www.linkedin.com/in/iamayushsaxena/)
- 🐙 **GitHub:** [iamayushsaxena](https://github.com/iamayushsaxena)
- 📧 **Email:** aysaxena8880@gmail.com

---

## 🙏 Acknowledgments

- **Problem Inspiration**: Real-world challenges in food delivery personalization
- **Educational Value**: Demonstrates end-to-end ML product development
- **Portfolio Purpose**: Showcases product thinking + technical execution for PM roles

---

## ⭐ Star This Repo

If you found this project helpful or impressive, please consider:
- ⭐ **Starring the repository** (helps others discover it)
- 🔄 **Sharing on LinkedIn** (tag me!)
- 💬 **Providing feedback** (open an issue with suggestions)
- 🍴 **Forking for your own research** (with attribution)

---

**⭐ Star this repository if you found it valuable!**

**💬 Questions? [Open an issue](https://github.com/iamayushsaxena/ML-Restaurant-Recommendations/issues)**

**🤝 Feedback? [Start a discussion](https://github.com/iamayushsaxena/ML-Restaurant-Recommendations/discussions)**

---

<div align="center">

*Built with product thinking😎, not just algorithms!*

</div>