# CS439-NBAProject
Clustering NBA Players Into Playstyle Archetypes Using Season Statistics

## 📊 Project Overview
This project applies unsupervised machine learning techniques to cluster NBA players into distinct playstyle archetypes based on their season statistics. Using K-Means clustering and PCA dimensionality reduction, we identify five key player roles that correspond to real basketball positions and playing styles.

## 🎯 Objectives
- Fetch and process NBA player statistics using the official NBA API
- Identify optimal number of clusters using Elbow Method and Silhouette Analysis
- Apply K-Means clustering to group players with similar playing styles
- Use PCA for visualization and interpretation of high-dimensional player data
- Validate archetype stability across multiple seasons (2023-24 and 2024-25)
- Map numeric clusters to interpretable basketball roles

## 🏀 Identified Archetypes
The analysis identifies **5 distinct player archetypes**:

1. **Primary Creator** - High usage, high assists (e.g., Luka Dončić, Stephen Curry)
2. **Rim Protector** - High rebounds and blocks (e.g., Rudy Gobert, Nikola Jokić)
3. **Floor Spacer** - High 3-point attempt volume (e.g., specialists and shooters)
4. **Role Player** - Low usage, supporting stats (e.g., Alex Caruso)
5. **Versatile** - Balanced statistics across categories (e.g., Jayson Tatum, Giannis Antetokounmpo)

## 📈 Features Used
The clustering algorithm uses **13 statistical features** that capture playstyle, not just skill level:

- **Scoring**: Points (PTS)
- **Playmaking**: Assists (AST), Assist Percentage (AST_PCT)
- **Defense/Size**: Rebounds (REB), Steals (STL), Blocks (BLK)
- **Efficiency**: Field Goal % (FG_PCT), 3-Point % (FG3_PCT), Free Throw % (FT_PCT), True Shooting % (TS_PCT)
- **Volume/Style**: Usage % (USG_PCT), 3-Point Attempts (FG3A), Free Throw Attempts (FTA)

## 🛠️ Technical Stack
- **Python 3.x**
- **Data Collection**: `nba_api`
- **Data Processing**: `pandas`, `numpy`
- **Machine Learning**: `scikit-learn` (KMeans, PCA, StandardScaler)
- **Visualization**: `matplotlib`, `seaborn`
- **Environment**: Jupyter Notebook

## 🚀 Installation
```bash
pip install nba_api pandas matplotlib seaborn scikit-learn
```

## 📋 Methodology

### 1. Data Collection
- Fetch per-game base and advanced statistics using NBA API
- Filter players with >15 minutes per game to focus on rotation-level players
- Combine base box-score stats with advanced metrics (Usage %, True Shooting %, etc.)

### 2. Optimal Cluster Selection
- Applied **Elbow Method** to identify the "elbow" in inertia vs. k
- Calculated **Silhouette Scores** for k = 2 to 8
- Selected **k = 5** as optimal balance between interpretability and statistical validity
  - Elbow appears around k = 5
  - Corresponds to typical basketball team structure (5 players on court)
  - Provides meaningful role differentiation

### 3. Clustering Pipeline
- **Preprocessing**: Impute missing values with median, standardize features
- **K-Means**: Cluster players into 5 groups (42 random seed for reproducibility)
- **PCA**: Reduce to 2D for visualization while preserving variance
- **Archetype Mapping**: Assign readable names based on cluster-level statistics

### 4. Validation
- Compare archetype distributions across 2023-24 and 2024-25 seasons
- Analyze stability of key roles (Primary Creator, Rim Protector, Floor Spacer)
- Verify that similar players cluster together (e.g., Jokić and Gobert as rim protectors)

## 📊 Visualizations
The project includes several key visualizations:

1. **Elbow Plot**: Shows inertia decrease as k increases
2. **Silhouette Score Plot**: Evaluates cluster quality for different k values
3. **PCA Scatter Plots (by Cluster)**: Shows numeric cluster assignments with labeled high-usage stars
4. **PCA Scatter Plots (by Archetype)**: Color-coded by basketball role with notable players labeled
5. **Heatmaps**: Display average statistics per archetype with color gradients
6. **Stability Analysis Tables**: Compare role statistics across seasons

## 🔍 Key Findings
- **K = 5 provides optimal clustering** based on elbow method and basketball domain knowledge
- **Archetypes are stable across seasons**, with Primary Creators, Rim Protectors, and Floor Spacers showing consistent stat profiles in both 2023-24 and 2024-25
- **Star players cluster predictably**: Point guards (Luka, Curry) → Primary Creators; Centers (Gobert) → Rim Protectors
- **PCA captures meaningful variance**: First 2 principal components explain significant variance while maintaining interpretability
- **Role differentiation is clear**: Heatmaps show distinct statistical profiles for each archetype

## 📁 Project Structure
```
Final Project/
│
├── NBA Final Project.ipynb    # Main Jupyter notebook with full analysis
├── README.md                   # This file
└── Screen Recording...mp4      # Demo video (optional)
```

## 👥 Usage
1. Open `NBA Final Project.ipynb` in Jupyter Notebook or JupyterLab
2. Run cells sequentially to reproduce the analysis
3. The pipeline automatically:
   - Fetches latest NBA data
   - Performs clustering
   - Generates visualizations
   - Displays statistical summaries

## 📝 Notes
- **Garbage Time Filtering**: Players with <15 MPG excluded to avoid stat inflation from low-leverage minutes
- **Season Format**: NBA API uses format "YYYY-YY" (e.g., "2024-25")
- **Reproducibility**: Random seed set to 42 for consistent results across runs
