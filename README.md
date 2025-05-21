# Movie Recommender System

## Overview

This project is a **Content-Based Movie Recommender System** that suggests movies similar to the one you like. The recommendation is based on textual metadata such as genres, keywords, cast, and crew information.

## Dataset Used

The datasets used are available on Kaggle:

* [TMDB Movie Metadata](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

These datasets are imported directly from Google Drive in the project.

## Project Workflow

### 1. Dataset Loading and Merging

* Two CSV files: `movies.csv` and `credits.csv` are loaded.
* These datasets are merged **on the basis of the 'title' column** to form a comprehensive dataset.
* Only the following useful columns are extracted:

  * `movie_id`
  * `title`
  * `overview`
  * `genres`
  * `keywords`
  * `cast`
  * `crew`

### 2. Data Preprocessing

#### 2a. Removing Null Values

* Rows with any null values in the selected columns are removed.

#### 2b. Removing Duplicate Values

* Duplicate entries are dropped to ensure clean data.

#### 2c. Converting 'genres' and 'keywords' to List

* These columns contain stringified JSON objects.
* Each string is parsed and converted into a list of genre/keyword names.

#### 2d. Selecting Top 3 Cast Members

* The `cast` column is processed to keep only the top 3 actors.

#### 2e. Extracting Director from Crew

* From the `crew` column, only the director's name is retained.

#### 2f. Removing Spaces in Names

* All spaces in multi-word names are removed (e.g., "Tom Hanks" -> "TomHanks") to treat them as single words in vectorization.

### 3. Tag Creation

* A new column `tags` is created by **concatenating**:

  * `overview`
  * `genres`
  * `keywords`
  * `cast`
  * `crew`
* The purpose is to combine all relevant textual data into one field.

### 4. Text Processing

#### 4a. Stemming

* The `tags` text is normalized using a stemming process.
* This reduces words to their base/root form (e.g., "loved" -> "love").
* This helps in capturing the essence of similar words.

### 5. Feature Extraction using Bag of Words

* A **CountVectorizer** is used to convert the `tags` into vectors.
* A high-dimensional matrix is created where each row corresponds to a movie and each column to a word.

### 6. Recommendation Function

* A cosine similarity matrix is computed between the vectors.
* Given a movie title, the system computes similarity scores and returns the **top 5 most similar movies**.

## Result

The recommender system is able to suggest similar movies based on content, giving users meaningful recommendations even without user rating data.

## How to Run

* Load the notebook: `Movie_Recommender_System.ipynb`
* Ensure the dataset is accessible via the provided Drive link.
* Run each cell sequentially to load data, preprocess, vectorize, and test the recommender function.

