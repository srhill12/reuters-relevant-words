# Reuters Corpus Money Category Analysis

This project involves analyzing news articles related to financial topics from the Reuters corpus using Natural Language Processing (NLP) techniques. The focus is on extracting and analyzing text data from the "money-fx" and "money-supply" categories, followed by calculating Term Frequency-Inverse Document Frequency (TF-IDF) values for each word in the corpus.

## Project Overview

The main objective of this project is to:

1. Retrieve all articles related to specific financial topics.
2. Process and analyze these articles using TF-IDF to determine the importance of various terms.
3. Provide functionality to search for documents containing specific terms.

## Project Structure

- **Text Data Extraction**:
  - Retrieve news articles from the "money-fx" and "money-supply" categories in the Reuters corpus.
  - Store the retrieved articles in a list for further processing.
  
- **TF-IDF Calculation**:
  - Use `TfidfVectorizer` from `sklearn` to convert the text into numerical features.
  - Compute the TF-IDF weights for each term in the corpus.
  - Store the TF-IDF values in a pandas DataFrame for easy analysis.
  
- **Document Retrieval**:
  - Implement a function to search through the documents and retrieve those containing specified terms.

## Requirements

- **Python 3.x**
- **NLTK**: The Natural Language Toolkit for text processing. Install it using pip:
  ```bash
  pip install nltk
  ```
- **Scikit-learn**: A machine learning library for the TF-IDF vectorizer. Install it using pip:
  ```bash
  pip install scikit-learn
  ```
- **Pandas**: A data analysis library for handling and manipulating DataFrames. Install it using pip:
  ```bash
  pip install pandas
  ```
- **NumPy**: A library for numerical computations, used here for handling arrays. Install it using pip:
  ```bash
  pip install numpy
  ```

## Setup

Before running the script, ensure that you have the necessary NLTK data packages installed. The script will download them if they are not already installed:

```python
import nltk
nltk.download("reuters")
nltk.download("punkt")
```

## Usage

### 1. Retrieve Financial Articles
- The script extracts all news articles from the Reuters corpus related to the "money-fx" and "money-supply" categories.
- Example:
  ```python
  categories = ["money-fx", "money-supply"]
  money_news_ids = [
      doc
      for doc in reuters.fileids()
      if categories[0] in reuters.categories(doc)
      or categories[1] in reuters.categories(doc)
  ]
  ```

### 2. TF-IDF Calculation
- Calculate the TF-IDF weights for terms in the retrieved articles to determine their importance.
- Example:
  ```python
  vectorizer = TfidfVectorizer(stop_words="english")
  X = vectorizer.fit_transform(money_news)
  words = list(vectorizer.get_feature_names_out())
  frequency = list(np.ravel(X.sum(axis=0)))
  money_news_df = pd.DataFrame({"Word": words, "Frequency": frequency})
  ```

### 3. Document Retrieval Function
- Implement a function called `retrieve_docs(terms)` that searches the "money_news_ids" list and retrieves the number of articles for a given word or group of words.
- Example:
  ```python
  def retrieve_docs(terms):
      result_docs = []
      for doc_id in money_news_ids:
          found_terms = [
              word
              for word in reuters.words(doc_id)
              if any(term in word.lower() for term in terms)]
          if len(found_terms) > 0:
              result_docs.append(doc_id)
      return result_docs
  ```

### 4. Example Output
- After running the analysis, the script prints out the top 10 terms with their TF-IDF weights.
- Example output:
  | Word   | Frequency  |
  |--------|------------|
  | said   | 54.918051  |
  | mln    | 51.533825  |
  | bank   | 49.568996  |
  | stg    | 47.236863  |
  | billion| 43.544274  |

## Conclusion

This project demonstrates how to process and analyze financial news articles from the Reuters corpus using TF-IDF. It provides insights into the most important terms within the corpus and allows for easy retrieval of documents containing specific terms. The analysis can be expanded to include more categories or refined for more specific queries depending on the needs of the user.
