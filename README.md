# 🎬 Movie Recommendation System

This project is a **Content-Based Movie Recommendation System** built using **Pandas, Scikit-Learn (TF-IDF & Cosine Similarity)**, and the **TMDB 5000 Movies Dataset**.  

It takes a movie title as input and recommends **10 similar movies** based on **genres, keywords, director, cast, and movie overview**.

---

## 🚀 Features
- Recommends movies similar to a given title.
- Handles typos in movie names (suggests closest matches).
- Weights features for better recommendations:
  - **Genres** (highest weight ×10)  
  - **Keywords** (medium weight ×5)  
  - **Director** (medium weight ×3)  
  - **Overview** (lowest weight ×2)  
- Saves similarity matrix (`similarity.pkl`) and processed data (`movies.pkl`) for reuse.
- Interactive CLI interface with option to exit.

---

## 📂 Dataset
- **TMDB 5000 Movies Dataset** (`tmdb_5000_movies.csv` and `tmdb_5000_credits.csv`).  
- Contains details about movies including:
  - Title, genres, keywords, cast, crew, overview, production companies.

---

## ⚙️ How It Works
1. **Data Preprocessing**
   - Merge movies and credits dataset.
   - Parse JSON-like strings (`genres`, `keywords`, `cast`, `crew`, `production_companies`) into lists.
   - Handle missing values.

2. **Feature Engineering**
   - Create a **soup** (combined text) for each movie:
     ```
     soup = 10*genres + 5*keywords + 3*director + 2*overview
     ```
   - This ensures **genres** influence recommendations more than other features.

3. **Vectorization**
   - Apply **TF-IDF Vectorizer** with `max_features=5000` and English stopwords removed.

4. **Similarity Computation**
   - Compute **cosine similarity** between all movies.

5. **Recommendation Function**
   - Find the closest match for the input movie (typo handling with `difflib`).
   - Retrieve the 10 most similar movies.
   - Return movie title, IMDb vote average, and release date.

6. **User Interaction**
   - Accepts movie title as input.
   - Typing `"quit"` exits the system.

---

## 🛠️ Installation & Usage

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/movie-recommendation-system.git
cd movie-recommendation-system
```

### 2. Install Dependencies
```bash
pip install pandas scikit-learn
```

### 3. Download Dataset
Place the following files in the project folder:
- `tmdb_5000_movies.csv`
- `tmdb_5000_credits.csv`

### 4. Run the Program
```bash
python main.py
```

### Example Run
```
Enter a movie title (or type 'quit' to exit): Inception

Recommendations:
        original_title       vote_average   release_date
1       Interstellar        8.2            2014-11-05
2       The Prestige        8.0            2006-10-19
3       Memento             8.1            2000-10-11
...
```

---

## 📦 Files in Project
- **main.py** → Main script with preprocessing, similarity computation, and interactive recommendation.
- **similarity.pkl** → Precomputed cosine similarity matrix.
- **movies.pkl** → Processed DataFrame with movie titles and features.
- **tmdb_5000_movies.csv** → Dataset file.
- **tmdb_5000_credits.csv** → Dataset file.

---

## 🔮 Future Improvements
- Add **Streamlit/Django web interface**.
- Include **user ratings (Collaborative Filtering)** for hybrid recommendations.
- Improve typo tolerance with **fuzzy matching** instead of difflib.

---

## 🙌 Credits
- Dataset: [TMDB 5000 Movies Dataset on Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)
- Built with ❤️ using Python, Pandas, and Scikit-Learn.
