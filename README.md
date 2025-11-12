*MSBA – Analytics for Unstructured Data | University of Texas at Austin*

---

### 📍 Project Overview

We built a **crowdsourced recommender system** from scratch using **8,000+ beer reviews** scraped from *BeerAdvocate.com*. Our system allows users to specify three **preferred attributes** (e.g., “fruity,” “hoppy,” “crisp”) and returns the top three beer recommendations using multiple recommendation techniques:

- **Bag-of-Words + Cosine Similarity**
- **Word Vector Embeddings (SpaCy)**
- **Custom Trained Word Embeddings (Gensim)**
- **Sentiment-Based Filtering**
- **Rating-Only Baseline Comparisons**

---

### 🎯 Goals

- Extract and process thousands of **unstructured text reviews**
- Use **text similarity + sentiment** to match beers with user preferences
- Compare **bag-of-words** and **word embeddings** as feature representations
- Train **custom word vectors** for domain-specific recommendation
- Evaluate the tradeoffs of **rating-based** vs. **text-driven** methods
- Identify similar products for a “competitor analysis” use case

---

### 📑 Dataset

- **Source**: *BeerAdvocate.com* Top 250 beers
- **Scraped**: ~8,000 reviews across ~250 unique beers
- **Fields**: `product_name`, `product_review`, `user_rating`
- **Preprocessing**:
    - Removed reviews with no text
    - Tokenized and cleaned reviews (stopword removal, lemmatization)
    - Built document-term matrix and sentiment scores

---

### 🔍 Methods by Task

### **Task A: Data Collection & Preprocessing**

- Used `BeautifulSoup` and `requests` for scraping
- Created structured DataFrame with reviews, ratings, and beer names
- Preprocessed using spaCy for lemmatization and token cleaning

### **Task B: Bag-of-Words Recommender**

- Modeled review content as a **bag-of-words vector**
- Performed **cosine similarity** between user attribute vector and all reviews
- Combined similarity with **sentiment scores** and **average ratings**
- Recommended top 3 beers with table of top 20 for transparency

### **Task C: Word Embedding Recommender**

- Replaced bag-of-words with **SpaCy’s pretrained word vectors**
- Averaged token embeddings to represent full reviews
- Recalculated cosine similarities for user attributes
- Compared performance and interpretability vs BoW

> Result: Word vectors captured semantic nuance but diluted specificity; bag-of-words performed better for sharply defined attributes like "crisp" or "malty"
> 

### **Task D: Custom Trained Embeddings**

- Trained **Gensim Word2Vec** on the 8k-review corpus
- Captured beer-specific semantics (e.g., “roasty” ↔ “smoky”, “bitter” ↔ “hoppy”)
- Replaced SpaCy embeddings in recommender pipeline
- Recommendations slightly shifted — more **niche** beers surfaced

### **Task E: Ratings-Only Baseline**

- Identified 3 highest-rated beers in the dataset
- Compared them against user-specified attributes
- Found that **rating-only ignores context** — top-rated beers often misaligned with user needs

### **Task F: “Beer Competitor” Analysis**

- Chose 10 random beers
- For a selected beer, used cosine similarity over review vectors to find its **nearest neighbor**
- Demonstrated how **competitive positioning** can be derived from review language similarity, not just ratings

---

### 📊 Sample Output (Task B)

| Rank | Beer Name | Avg Rating | Similarity Score | Final Score |
| --- | --- | --- | --- | --- |
| 1 | Bourbon County Stout | 4.65 | 0.82 | 0.87 |
| 2 | Julius IPA | 4.57 | 0.79 | 0.84 |
| 3 | Pliny the Elder | 4.61 | 0.77 | 0.83 |
| ... | ... | ... | ... | ... |

---

### 🧠 Key Takeaways

- **Bag-of-Words** excels when attributes are **explicit and specific**
- **Word embeddings** generalize well but can blur precision for niche descriptors
- **Sentiment and similarity fusion** adds interpretability and human alignment
- **Custom embeddings** give the best results when review language is highly domain-specific
- Ratings-only models are insufficient for nuanced recommendations

---

### 💡 Skills & Tools Applied

| Domain | Tools / Skills |
| --- | --- |
| **Web Scraping** | `BeautifulSoup`, `requests` |
| **Text Processing** | `spaCy`, `nltk`, `pandas` |
| **Modeling** | Cosine similarity, sentiment scoring, Gensim Word2Vec |
| **Evaluation** | Comparative ranking tables, lift analysis |
| **Recommendation Logic** | Attribute–review matching, hybrid scoring models |
