# 🎬 Movie Recommender

A movie recommendation web app. Search for any movie, open its details page, and get similar movie suggestions.

- **Backend:** FastAPI
- **Frontend:** Streamlit
- **ML / NLP:** Text preprocessing → TF-IDF vectorization → Cosine similarity
- **Dataset:** TMDB `movies_metadata.csv` (Kaggle)
- **Posters and live data:** TMDB API

---

## ✨ Features

- Home feed with Trending, Popular, Top Rated, Now Playing and Upcoming movies
- Search by keyword with dropdown suggestions and a poster grid
- Movie details page (poster, release date, genres, overview, backdrop)
- Two types of recommendations:
  - **Similar Movies (TF-IDF):** content-based, using cosine similarity
  - **More Like This (Genre):** popular movies from the same genre via TMDB

---

## 🧠 How the Recommendation Works

1. Load `movies_metadata.csv` and clean it (remove missing values and duplicates).
2. Preprocess the text (lowercase, remove punctuation and stopwords).
3. Convert the text into numbers using **TF-IDF**.
4. Compare the selected movie with every other movie using **cosine similarity**.
5. Return the top N movies with the highest similarity score.

The trained files are saved as pickle files and loaded when the API starts:

`df.pkl`, `indices.pkl`, `tfidf_matrix.pkl`, `tfidf.pkl`

---

## 📁 Project Structure

```
├── backend/
│   ├── main.py             # FastAPI app
│   ├── df.pkl
│   ├── indices.pkl
│   ├── tfidf_matrix.pkl
│   ├── tfidf.pkl
|   ├── requirements.txt
│   └── .env                # TMDB_API_KEY
├── frontend/
│   └── app.py              # Streamlit app
└── README.md
```

> Change the file names if yours are different.

---

## ⚙️ Setup

### 1. Clone the repo

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Get a TMDB API key

Create a free account at [themoviedb.org](https://www.themoviedb.org/), get an API key, and create a `.env` file inside the backend folder:

```
TMDB_API_KEY=your_api_key_here
```

---

## 🚀 Run the Project

**Start the backend (Terminal 1):**

```bash
cd backend
uvicorn main:app --reload
```

API runs at `http://127.0.0.1:8000`. API docs are at `http://127.0.0.1:8000/docs`.

**Start the frontend (Terminal 2):**

```bash
cd frontend
streamlit run app.py
```

App opens at `http://localhost:8501`.

> To use your local backend, set `API_BASE = "http://127.0.0.1:8000"` in `app.py`.

---

## 🔌 API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /health` | Check if the API is running |
| `GET /home?category=popular&limit=24` | Home feed (trending, popular, top_rated, now_playing, upcoming) |
| `GET /tmdb/search?query=batman` | Search movies by keyword |
| `GET /movie/id/{tmdb_id}` | Movie details |
| `GET /recommend/genre?tmdb_id=123` | Genre-based recommendations |
| `GET /recommend/tfidf?title=Toy Story` | TF-IDF recommendations (title and score) |
| `GET /movie/search?query=Toy Story` | Details + TF-IDF + genre recommendations in one call |

---

## 🛠 Tech Stack

Python, FastAPI, Uvicorn, Streamlit, Pandas, NumPy, Scikit-learn, HTTPX, TMDB API

---

## 🔮 Future Improvements

- Hybrid recommendations (content-based + collaborative)
- Better embeddings (Word2Vec / BERT)
- User login and watchlist
