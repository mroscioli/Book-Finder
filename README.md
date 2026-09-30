# Book Finder: NLP-Based Book Recommendation System

## Overview

**Book Finder** is a book recommendation system developed using **Natural Language Processing (NLP)** techniques to analyze and compare the plots of books.

The project uses a dataset of **16,559 books collected from Wikipedia**, containing information such as title, author, genre, publication date, and plot. The main goal is to process the textual content of book plots, identify recurring thematic structures, and use text similarity to recommend books based on a user's description or a selected book.

The project was developed using **Google Colab, Jupyter Notebook, and Spyder**.

---

## Objectives

The main objectives of the project were:

* Clean and preprocess a large collection of book plots.
* Identify the main thematic structures within the corpus using **Topic Modeling**.
* Represent book plots numerically using **TF-IDF**.
* Measure the similarity between books and user-provided descriptions.
* Build a recommendation system capable of suggesting relevant books.
* Provide two different ways to obtain recommendations: through a short description or through an existing book title.

---

## Dataset

The dataset contains **16,559 books from Wikipedia** and includes the following information:

* **Book title**
* **Author**
* **Genre**
* **Publication date**
* **Plot**
* Wikipedia and Freebase identifiers

During the data preparation phase, the `Wikipedia_article_ID` and `Freebase_ID` variables were removed because they were not required for the analysis.

Missing values in fields such as genre, publication date, and author were retained and replaced with `"Unknown"` where necessary. The `Book_genres` variable was also transformed from a dictionary format into a list of genres.

---

## Project Workflow

The project was developed through five main stages:

1. **Data Loading and Cleaning**
2. **Text Preprocessing**
3. **Topic Modeling**
4. **Text Representation and Similarity Analysis**
5. **Book Recommendation**

---

## 1. Text Preprocessing

The book plots were cleaned and transformed before being used for NLP analysis.

The preprocessing pipeline included:

* Removal of non-alphanumeric characters and special symbols
* Conversion of text to lowercase
* **Stopword removal**
* **Stemming**
* **Lemmatization**
* Removal of one-character words
* **Bigram extraction** using Gensim

Bigrams were identified using the Gensim `Phrases` model, with:

* `min_count = 5`
* `threshold = 20`

These preprocessing steps substantially reduced the average number of words per plot while retaining the most relevant textual information.

---

## 2. Topic Modeling with LDA

To explore the main thematic structures present in the book corpus, **Latent Dirichlet Allocation (LDA)** was applied.

A dictionary and corpus were created from the preprocessed texts, and a **TF-IDF corpus** was also generated.

### Hyperparameter Search

A Grid Search was performed by testing models with between **1 and 24 topics**.

The models were evaluated using:

* **Perplexity**
* **Coherence Score**

Coherence was used as the main criterion for selecting the final model.

The selected model used:

* **22 topics**
* **Asymmetric alpha**
* **Beta = 0.31**
* **10 iterations**
* Coherence score of approximately **0.554**

The analysis also showed that some of the later topics had considerable overlap, particularly among **fantasy and science-fiction-related themes**, while the first topics were more clearly differentiated.

**pyLDAvis** was used to visually explore the relationships and overlap between the identified topics.

---

## 3. TF-IDF Text Representation

To compare book plots and identify similar books, the texts were transformed into numerical vectors using **TF-IDF (Term Frequency–Inverse Document Frequency)**.

A `TfidfVectorizer` was used to create a sparse matrix representing the textual characteristics of each book.

This representation allows the system to compare the importance of words across different plots while reducing the influence of very common terms.

---

## 4. Cosine Similarity

After transforming the plots into TF-IDF vectors, **cosine similarity** was used to measure the similarity between texts.

The system can compare:

* A **user-provided description** with all book plots
* A **selected book** with the other books in the dataset

The books with the highest similarity scores are then returned as recommendations.

---

## 5. Recommendation System

The final system provides two recommendation modes.

### Search by Description

The user can enter a short description of the type of story they are looking for.

The description is transformed using the same TF-IDF representation used for the book plots. Cosine similarity is then calculated against the entire collection to identify the most relevant books.

### Search by Book Title

The user can also enter the title of a book already present in the dataset.

The system compares its plot with the plots of the other books and returns the most similar titles.

The user can also specify the **number of recommendations** to receive.

If the requested title is not available in the dataset, the system returns an appropriate message instead of generating recommendations.

---

## Methodology

The overall workflow can be summarized as:

```text
Raw Book Dataset
       ↓
Data Cleaning
       ↓
Text Preprocessing
       ↓
Stopword Removal
       ↓
Stemming + Lemmatization
       ↓
N-gram Extraction
       ↓
LDA Topic Modeling
       ↓
TF-IDF Representation
       ↓
Cosine Similarity
       ↓
Book Recommendations
```

---

## Technologies and Libraries

The project was developed using **Python** and the following tools and libraries:

* **Python**
* **Pandas**
* **NumPy**
* **NLTK**
* **Gensim**
* **Scikit-learn**
* **Matplotlib**
* **pyLDAvis**
* **Google Colab**
* **Jupyter Notebook**
* **Spyder**

---

## Key Results

The project demonstrated how NLP techniques can be applied to a large collection of literary texts to extract thematic information and build a content-based recommendation system.

The main results include:

* Identification of **22 main topics** using LDA.
* A final LDA coherence score of approximately **0.554**.
* Representation of book plots using **TF-IDF**.
* Similarity analysis based on **cosine similarity**.
* A recommendation system supporting both **description-based** and **book-based** searches.

---

## Possible Future Improvements

Several extensions could further improve the system:

* Experimenting with **word embeddings** such as Word2Vec, FastText, or transformer-based representations.
* Testing more advanced semantic similarity techniques.
* Combining plot-based recommendations with **genre, author, and rating information**.
* Developing a more advanced hybrid recommendation system.
* Creating a web-based interface for easier interaction with the recommender.

---

## Project Context

This project was developed as part of a university data science project, with a focus on **Natural Language Processing, text analysis, topic modeling, and recommendation systems**.
