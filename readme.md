# Machine Learning Project Report - I Dewa Gede Mahesta Parawangsa
This Recommendation System project develops a content-based filtering model to generate top-N book recommendations and utilizes K-Means clustering to analyze book groupings based on their features.

## Project Overview

<img src="https://github.com/user-attachments/assets/0fc41268-0865-4095-b6dd-7e11e691f1ca" alt="Buku Self Development" width="600">

<br>[Image Reference](https://digitalskola.com/blog/home/buku-self-development)

Book Recommendation System
*Concept of a Book Recommendation System (Source: Adapted from various sources)*

In the current era, which is synonymous with the age of literacy, the ability to access and utilize knowledge is crucial, especially for young intellectuals as agents of change in facing global challenges [[1](https://jurnal.unissula.ac.id/index.php/ELIC/article/view/1282/)]. Libraries, as centers for book collections and reading materials, play an important role in supporting literacy and providing information [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

However, as library collections and information systems like the *Online Public Access Catalog* (OPAC) grow, visitors often face difficulties. Current systems generally only display basic information about the searched book and are not yet able to suggest other relevant or similar books [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)]. Visitors need more time to find alternatives when the desired book is unavailable or when they want to explore similar titles.

To address this challenge, this project develops a **Book Recommendation System**. This system aims to help users filter information and find books that are most likely to be of interest to them [[3](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [4](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)]. The main approach implemented is **Content-Based Filtering**, which recommends books based on the similarity of their features or content, such as `title`, `authors`, `categories`, and `published_year` [[3](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System)]. This approach is effective even when user rating data is limited because it utilizes book metadata [[5](https://www.researchgate.net/publication/317382367_Amazon_Everything_you_wanted_to_know_about_its_algorithm_and_innovation)].

To improve the quality of recommendations and address the potential *cold start problem* (difficulty recommending new items or to new users) [[6](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [7](https://www.researchgate.net/publication/221563070_Amazoncom_recommendations_item-to-item_collaborative_filtering)], this project also integrates **Collaborative Filtering**, specifically the **User-Based CF** method. This approach works by analyzing rating patterns from many users to find users with similar tastes and then recommending books liked by that *peer group* [[8](https://www.researchgate.net/publication/327890511_A_Comparison_Study_Between_Content-Based_and_Popularity-Based_Filtering_via_Implementing_a_Book_Recommendation_System), [9](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)]. By combining these two methods (a Hybrid System), it is expected that the system can provide more accurate, diverse, and relevant recommendations, as has been successfully implemented by platforms like Netflix [[10](https://dl.acm.org/doi/10.1145/2843948)] and Amazon [[11](https://ieeexplore.ieee.org/document/1167344), [2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

The implementation of this recommendation system is expected to improve the quality of library services (or other book platforms), make it easier for users to find books that match their interests, shorten search time, and overall enhance the reading experience and support a culture of literacy [[2](https://download.garuda.kemdikbud.go.id/article.php?article=2044898&val=13150&title=Sistem%20Rekomendasi%20Buku%20pada%20Perpustakaan%20Daerah%20Provinsi%20Kalimantan%20Selatan%20Menggunakan%20Metode%20Content-Based%20Filtering)].

## Business Understanding

This section will explain the background of the problem, the goals to be achieved through this book recommendation system project, and the solution approach that will be used.

### Problem Statements

The main problems that drive the development of this book recommendation system are:

1.  **Difficulty in Finding Relevant Books (Information Overload):**
    *   Modern libraries and digital book platforms have vast and constantly growing collections.
    *   Users often feel overwhelmed by the sheer number of choices and find it difficult to discover books that truly match their specific interests or needs among the thousands or millions of available titles.
    *   Manual searching or browsing by general categories is often inefficient and time-consuming.

2.  **Difficulty in Finding Similar Books:**
    *   After finishing a book they enjoyed, users often want to read other books with a similar theme, writing style, genre, or author.
    *   Existing library catalogs or online bookstores may not effectively suggest these similar books, forcing users to perform additional searches that may not be fruitful.

3.  **Lack of Personalization and Discovery (Serendipity):**
    *   Users tend to search for or choose books from authors or genres they are already familiar with, limiting their exploration of new or different titles they might also enjoy.
    *   The book discovery experience is often generic and not tailored to the unique preferences of each individual, reducing the chance of *serendipity* (a pleasant, unexpected discovery).

4.  **Limitations of Current Library/Platform Information Systems:**
    *   Existing *Online Public Access Catalog* (OPAC) systems or similar platforms often only provide basic search functions (by title, author, ISBN) and descriptive book information, without the proactive ability to suggest other relevant items.
    *   This results in a suboptimal user experience and causes potentially relevant but less popular books in the collection to remain hidden.

### Goals

Based on the problems above, the main goals of this book recommendation system project are:

1.  **To Improve the Efficiency of Book Discovery:**
    *   Develop a system that can help users filter through large book collections and quickly find titles that are most likely to match their preferences, addressing *Problem Statement 1*.

2.  **To Provide Relevant and Similar Book Recommendations:**
    *   Build a model capable of identifying and suggesting other books that have similar content (genre, theme, author, etc.) or user interest patterns (based on other users' ratings) to the book a user is currently viewing or likes, addressing *Problem Statement 2*.

3.  **To Enhance Personalization and Facilitate New Book Discovery:**
    *   Provide more personalized recommendations tailored to each user's unique tastes, and help them discover interesting books outside their comfort zone (increasing *serendipity*), addressing *Problem Statement 3*.

4.  **To Enhance Existing Information System Services:**
    *   Add recommendation functionality to existing book search systems (like OPACs or digital platforms) to improve the overall quality of service and user experience, addressing *Problem Statement 4*.

### Solution Statements

To achieve these goals, the following solution approaches will be implemented and evaluated:

1.  **Content-Based Filtering:**
    *   Develop a model that analyzes the intrinsic features of a book (such as `title`, `authors`, `categories`, `published_year`, and possibly `description`).
    *   Use techniques like **TF-IDF (Term Frequency-Inverse Document Frequency)** to represent the book's content as a numerical vector.
    *   Calculate the similarity between books using a metric like **Cosine Similarity** based on these feature vectors.
    *   Recommendations are generated by suggesting books that are most similar in content to a book the user likes.

2.  **Collaborative Filtering (User-Based):**
    *   Implement a model that utilizes historical rating data or user interactions with books (`average_rating`, `ratings_count`, or ideally, per-user rating data).
    *   Identify users who have similar rating patterns or preferences to the target user.
    *   Recommend books that are liked (have high ratings) by these similar users but have not yet been read or rated by the target user. A possible method is **K-Nearest Neighbors (KNN)** on the user-item matrix or calculating **User Similarity** (e.g., Cosine Similarity between user rating vectors).

3.  **Hybrid Approach (Combination):**
    *   Combine the results from Content-Based Filtering and Collaborative Filtering to generate the final recommendations.
    *   Combination strategies could include:
        *   **Weighted Hybrid:** Assigning weights to the scores from each method.
        *   **Switching Hybrid:** Using one method depending on the context (e.g., CF for old users, CB for new users/new books).
        *   **Mixed Hybrid:** Displaying recommendations from both systems simultaneously.
    *   The goal of a hybrid system is to leverage the strengths of each approach and cover their weaknesses (e.g., overcoming the *cold start problem* of CF with CB).

## Data Understanding

### EDA - Variable Description

| Type       | Description                                                                                                    |
|------------|----------------------------------------------------------------------------------------------------------------|
| Title      | Books Dataset                                                                                                  |
| Source     | [Kaggle](https://www.kaggle.com/datasets/abdallahwagih/books-dataset/code/)                                      |
| Maintainer | [Abdallah Wagih](https://www.kaggle.com/abdallahwagih)                                                            |
| License    | Community Data License Agreement - Sharing - Version 1.0                                                       |
| Visibility | Public                                                                                                         |
| Tags       | books, recommendation system, chatbot development, literature, classification, clustering                      |
| Usability  | 10.00                                                                                                           |

Dataset Information: This dataset is a comprehensive collection of information about books, gathered from various sources and designed for use in recommendation systems and chatbot development. It includes details on a wide variety of books, making it suitable for various applications in machine learning, natural language processing, and artificial intelligence. The dataset used in this project is publicly available on Kaggle under the name: _Books Dataset_. It can be downloaded here: [Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset/code/).

**Dataset Information**:
 - The dataset is an `.xlsx` file (Excel Spreadsheet).
 - The dataset consists of 1 XLSX file: `book.xlsx`.
 - The dataset has **6810 samples** (rows of data) with **12 initial features**.
 - The dataset has 4 `float64` features, 1 `int64` feature, and 7 `object` features.
 - There are *Missing values* in several initial features such as `subtitle` (significant), `authors`, `categories`, `thumbnail`, `description`, `published_year`, `average_rating`, `num_pages`, and `ratings_count`. However, after *data preparation* (cleaning and imputation/type conversion), the key features used for *content-based filtering* (`title`, `authors`, `categories`, `published_year`, `combined_features`) **have no missing values**.
 - There is no duplicate data in the dataset.

### Variables in the Dataset

Here is a brief explanation for each column in the book.xlsx dataset:

*   **`isbn13`**: The 13-digit ISBN (International Standard Book Number), a unique international identifier for the book. (Removed during Data Preparation).
*   **`isbn10`**: The 10-digit ISBN, a unique book identifier (the older standard before ISBN-13). It is an `object` (text) type because it can contain the character 'X'. (Removed during Data Preparation).
*   **`title`**: The main title of the book. *Used as a feature.*
*   **`subtitle`**: The subtitle or additional title of the book (this column has many null values).
*   **`authors`**: The name of the author or authors of the book. Can contain more than one name. *Used as a feature.*
*   **`categories`**: The category or genre of the book (e.g., Fiction, History, Computers). Can contain more than one category. *Used as a feature.*
*   **`thumbnail`**: A URL link to a small cover image (thumbnail) of the book. (Removed during Data Preparation).
*   **`description`**: A summary, synopsis, or brief description of the book's content.
*   **`published_year`**: The year the book was first published. (Initially a `float64`, cleaned and converted to a string). *Used as a feature.*
*   **`average_rating`**: The average rating score given by users for the book (the scale is not standard and would need normalization if used).
*   **`num_pages`**: The total number of pages in the book. (Initially a `float64`).
*   **`ratings_count`**: The total number of users who have given a rating to the book. (Initially a `float64`).
*   **`combined_features`**: A new column created during *data preparation*, containing the combined text from `title`, `authors`, `categories`, and `published_year` after cleaning. This is the main input for TF-IDF.

### Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) was conducted to gain a deep understanding of the characteristics and distribution of the data in the book dataset (`book.xlsx`). This EDA helps to identify patterns, anomalies, and biases in the data that could affect the development of the recommendation system. Here are the key findings:

1.  **Distribution of Book Categories:**
    ![image](https://github.com/user-attachments/assets/579a7e0f-8de2-4922-a27e-106f2f472237)
    *   **Visualization:** A bar chart showing the top 10 book categories by frequency.
    *   **Observations:**
        *   **Dominance of Fiction:** The **Fiction** category is highly dominant, appearing over 2500 times, far surpassing other categories.
        *   **Next Popular Categories:** Juvenile Fiction and Biography & Autobiography are in second and third place with frequencies of about 540 and 400 times, respectively.
        *   **Data Imbalance:** Other popular categories (like `history`, `literary criticism`, etc.) appear with much lower frequencies.
    *   **Interpretation:** This highly imbalanced distribution of categories is important to note. It could potentially cause the recommendation model to be biased towards recommending fiction books over less represented categories, unless handled specifically in the modeling.

2.  **Publication Year Trends:**
    ![image](https://github.com/user-attachments/assets/f954c04f-30de-4763-9b79-4aa7f07e1ba6)

    *   **Visualization:** A histogram showing the distribution of the number of books published per year.
    *   **Observations:**
        *   **Concentration in the Modern Era:** Most books in the dataset were published in the last few decades.
        *   **Peak of the Distribution:** The largest number of books were published around the **early 2000s**.
        *   **Left-Skewed Distribution:** There is a long "tail" to the left, indicating a much smaller number of books from earlier years (e.g., before 1975).
        *   **Significant Increase:** The number of book publications began to increase significantly around the 1970s.
    *   **Interpretation:** The dataset is dominated by relatively modern books. The recommendation system might be more effective at recommending new books or those published after the 1970s due to the richer data representation for that period.


3.  **Author Popularity:**
    ![image](https://github.com/user-attachments/assets/cdb33eaa-ceb6-4d76-b038-155d584df720)
    *   **Visualization:** A bar chart showing the top 10 authors with the most books in the dataset.
    *   **Observations:**
        *   **Top Authors:** **Agatha Christie** and **Stephen King** have the most books represented (each with over 35 books). William Shakespeare is also highly represented.
        *   **Other High Representations:** Other popular authors like J.R.R. Tolkien, Virginia Woolf, and Sandra Brown also have a significant number of books (generally between 17 and 26).
    *   **Interpretation:** The dataset is biased towards very popular and prolific authors. The recommendations generated might tend to repeat these authors unless a mechanism to increase author diversity is implemented.



4.  **Distribution of Average Ratings:**
    ![image](https://github.com/user-attachments/assets/55423b12-730c-48a1-84fa-4e8ce9aadc27)
    *   **Visualization:** A histogram showing the distribution of average book ratings. *Note: The scale on the X-axis (0-500) does not seem to correspond to a standard book rating scale (e.g., 1-5). This needs to be considered.*
    *   **Observations:**
        *   **Bimodal Distribution:** There are two main peaks in the distribution.
        *   **High Rating Peak:** The main peak (majority of books) is around a **rating of 380-420** (on the displayed 0-500 scale), indicating a tendency for books to have high ratings on that scale.
        *   **Small Low Rating Peak:** There is a much smaller second peak around a rating of 0-50, suggesting a group of books with very low ratings.
    *   **Interpretation:** The presence of two rating groups (high and low) is interesting. However, the **non-standard rating scale (0-491?) requires clarification or normalization** before this feature can be used effectively in modeling, as interpreting its absolute value is difficult. The bimodal pattern might indicate segments of highly liked and highly disliked books.



5.  **Distribution of Number of Pages:**
    ![image](https://github.com/user-attachments/assets/d18202a3-8504-4dfe-a478-d35d4291ef17)
    *   **Visualization:** A box plot showing the spread of the number of pages in books.
    *   **Observations:**
        *   **Main Concentration (The Box):** 50% of the books in the middle of the dataset have between approximately 150-200 and 350-400 pages.
        *   **Median:** The line inside the box (median) is around 250-300 pages, meaning half the books have fewer pages than this, and half have more.
        *   **Many Outliers:** There are a great number of points (*outliers*) to the right of the whisker, indicating a significant number of books with a very high page count (can reach over 1000, 2000, or even 3000 pages).
        *   **Right-Skewed Distribution:** The presence of these many outliers makes the distribution of the number of pages highly right-skewed.
    *   **Interpretation:** Most books have a standard length, but the presence of very thick books as significant outliers is noteworthy. If the number of pages feature is used in modeling (e.g., for clustering), the influence of these outliers needs to be considered, and using an outlier-resistant scaling technique (like `RobustScaler`) might be necessary.



6.  **Uniqueness of Titles:**
    *   **Observation:** Out of a total of 6810 book entries, there are 6397 unique titles.
    *   **Percentage:** This means **93.9%** of the books in the dataset have a different title from one another.
    *   **Interpretation:** This high level of title uniqueness indicates good data quality in terms of book identification and minimal duplication of records based on the exact same title. This makes it easier to match user-input titles with the existing data.

    ```
    Unique Titles: 6397/6810 (93.9%)
    ```

## Data Preparation

The Data Preparation stage is a crucial step to ensure that the data used to build this book recommendation system is of high quality and ready for processing. Since this system focuses on content similarity (Content-Based Filtering), data preparation is aimed at cleaning and combining relevant textual features (like title, authors, categories, and publication year) into a single representation that can be processed by the TF-IDF model. This process also involves handling missing values in key features and removing columns that are not relevant for calculating content similarity. Based on the code analysis in the notebook, here are the data preparation steps that were performed:

### 1. Cleaning Text Features (`title`, `authors`, `categories`)

*   **Process:**
    *   An iteration was performed on the selected text features (`title`, `authors`, `categories`).
    *   Each feature was converted to the string data type for consistency.
    *   All characters that are not alphanumeric (letters and numbers) or spaces were removed using a regular expression (`[^a-zA-Z0-9\\s]`).
    *   All text was converted to lowercase (`lower()`) to eliminate case sensitivity.
*   **Reason:**
    *   **Standardization:** Converting all text to lowercase and removing non-alphanumeric characters ensures that the same words (e.g., "Fiction" and "fiction") or variations due to punctuation are not treated as different by the TF-IDF algorithm.
    *   **Noise Reduction:** Removing punctuation and symbols reduces "noise" in the text data that can interfere with word frequency and similarity calculations.
    *   **Preparation for Tokenization:** Clean text is easier to split into word units (tokens) in the vectorization step.

### 2. Cleaning and Converting the `published_year` Feature

*   **Process:**
    *   The `published_year` column was converted to the string data type.
    *   All characters that are not digits (numbers) were removed.
    *   Any empty strings that might result (if the original value was invalid or missing) were replaced with '0'.
    *   The result was converted to an integer type (to ensure numerical validity) and then converted back to a string type.
*   **Reason:**
    *   **Format Consistency:** Ensures that the publication year column has a consistent numeric string format, free from non-numeric characters or non-standard date formats.
    *   **Feature Combination:** Converting it to a string allows the publication year to be combined with other text features and treated as a "word" or token representing the publication era in the TF-IDF analysis.
    *   **Implicit Missing Value Handling:** By replacing empty strings (resulting from non-numeric or original NaN values) with '0', this implicitly handles potential missing or invalid values in this column before the final conversion to a string.

### 3. Combining Features (`combined_features`)

*   **Process:**
    *   A new column named `combined_features` was created.
    *   The value in this column is the result of concatenating the cleaned strings from the `title`, `authors`, `categories`, and `published_year` columns, with a space as a separator between features.
*   **Reason:**
    *   **Single Content Representation:** Creates a single, comprehensive textual representation for each book, which includes the main content information from key features.
    *   **Input for TF-IDF:** This `combined_features` column becomes the primary input ("document") for the TfidfVectorizer. Vectorization will be performed on this combined text to capture the overall content profile of each book in the form of a numerical vector.

### 4. Handling Missing Values in Key Features (Safeguard)

*   **Process:**
    *   Although the previous cleaning steps effectively handle missing values in `title`, `authors`, `categories`, and `published_year` (e.g., by converting NaN to the string 'nan' or '0' for the year), the code `df.dropna(subset=selected_features, how='any')` was run.
    *   This step would theoretically remove any row that *still* has a missing value in *any* of the selected key features (`selected_features`).
*   **Reason:**
    *   **Core Data Integrity:** While the previous cleaning steps were effective (as seen in the `df.isnull().sum()` output showing 0 missing values for these features), this `dropna` step serves as a **safeguard layer** to ensure there are absolutely no missing values in the most crucial features (`title`, `authors`, `categories`, `published_year`) before they are used to create `combined_features` and fed into the model. This guarantees that every book entering the vectorization stage has a complete basic content profile.

### 5. Removing Unnecessary Columns

*   **Process:** The `isbn13`, `isbn10`, and `thumbnail` columns were removed from the DataFrame.
*   **Reason:**
    *   **Relevance for the Model:** These columns (unique book identification numbers and an image link) do not directly provide information about the book's *content* that is relevant for a content-based filtering approach using TF-IDF on textual features.
    *   **Efficiency:** Removing unused columns makes the dataset more concise and focuses the analysis on the features that actually contribute to the content similarity calculation.

## Modeling

In this stage, a book recommendation system model was developed based on the prepared data. The main goal is to provide relevant book recommendations to users. In this project, two different recommendation approaches or solutions are presented:

1.  **Pure Content-Based Filtering (CBF):** Using content similarity between books.
2.  **Content-Based Recommendation Enhanced with Clusters (CBF + K-Means):** Combining content similarity with information from book clustering to provide potentially more diverse or popular additional recommendations.

Both approaches were built to address the problem of finding books that match user preferences.

### 1. Content-Based Filtering (TF-IDF & Cosine Similarity)

The first approach is a pure content-based recommendation system. The basic idea is to recommend books that have similar features or content to books a user has liked in the past or a book they are currently viewing.

**Implementation:**

1.  **Combining Content Features:** Relevant textual and categorical features like `title`, `categories`, `authors`, and `published_year` were combined into a single text representation for each book. This created a comprehensive description of each book's content.
2.  **TF-IDF Vectorization:** The combined text was then converted into a numerical vector representation using `TfidfVectorizer` from `sklearn`. TF-IDF (Term Frequency-Inverse Document Frequency) measures how important a word is in a document (book) relative to the entire collection of documents (all books). The result is a TF-IDF matrix where each row represents a book and each column represents a unique word, with the cell value being the TF-IDF score.
3.  **Cosine Similarity:** The similarity between books was calculated based on their TF-IDF vectors using the Cosine Similarity metric. This metric measures the cosine of the angle between two vectors, resulting in a score between 0 (not similar) and 1 (very similar). A square similarity matrix was generated, where `similarity[i][j]` indicates the similarity score between the i-th and j-th book.
4.  **Providing Top-N Recommendations:** When a user provides a book title as input, the system finds the closest match in the dataset, retrieves the corresponding row of similarity scores from the similarity matrix, sorts them in descending order, and presents the top N books (excluding the input book itself) as recommendations.

**Example of Top-5 Recommendations (for input 'Gilead'):**

| Rank | Title            | Authors               | Categories   | Published Year | Cosine Similarity |
| :--- | :--------------- | :-------------------- | :----------- | :------------- | :---------------- |
| 1    | the martians     | kim stanley robinson  | fiction      | 2000           | 0.32              |
| 2    | robinson crusoe  | daniel defoe          | fiction      | 2003           | 0.31              |
| 3    | kilo class       | patrick robinson      | fiction      | 1999           | 0.31              |
| 4    | uss seawolf      | patrick robinson      | fiction      | 2001           | 0.30              |
| 5    | pacific edge     | kim stanley robinson  | fiction      | 1995           | 0.30              |

**Advantages of Content-Based Filtering:**

*   **No Need for Other Users' Data:** Recommendations are made based on an item's profile and a single user's preferences, not depending on other users' data (addressing the *user cold-start* problem).
*   **Transparency:** It's relatively easy to explain why an item was recommended (because it's similar to other liked items).
*   **Can Recommend New/Unpopular Items:** As long as an item has an adequate feature description, it can be recommended even if no one has rated it yet (addressing the *item cold-start* problem).

**Disadvantages of Content-Based Filtering:**

*   **Limited Content Analysis:** Requires good item feature data. If features are not descriptive enough or are hard to extract (e.g., writing quality, plot nuances), the quality of recommendations decreases.
*   **Overspecialization:** Tends to recommend items that are very similar to what a user already likes, making it hard to discover items from completely new genres or types (*low serendipity*).
*   **Requires Domain Knowledge:** The process of *feature engineering* (selecting and combining features) often requires good domain knowledge.

### 2. Content-Based Recommendation Enhanced with Clusters (CBF + K-Means)

The second approach aims to add another dimension to the recommendations by leveraging the group structure within the book data. In addition to providing recommendations based on pure content similarity, this approach also considers the popularity or characteristics of book clusters.

**Implementation:**

1.  **Selecting Clustering Features:** Numerical features reflecting popularity or general book characteristics like `average_rating`, `num_pages`, and `ratings_count` were selected.
2.  **Feature Scaling:** These features were scaled using `RobustScaler` so that their values are in a comparable range and not dominated by features with large scales. RobustScaler was chosen for its resistance to outliers.
3.  **K-Means Clustering:** The K-Means algorithm was applied to the scaled feature data to group the books into clusters. Based on the Elbow Method and Silhouette Score analysis, the optimal number of clusters (k) was set to 2. The result of this clustering (e.g., Cluster 0 and Cluster 1) was then added as a new feature to the main DataFrame. In this project, these clusters were interpreted as representing, for example, "Underrated" books (Cluster 0) and "Best Seller / Popular" books (Cluster 1).
4.  **Providing Combined Recommendations:** The `recommend_with_cluster_info` function was developed. This function:
    *   Takes a book title as input and determines its cluster.
    *   Displays Top-N recommendations based on pure **content similarity (CBF)** (same as the first approach).
    *   Separately, it identifies books from the **"popular" cluster (Cluster 1)**, calculates their content similarity to the input book (using the CBF similarity matrix), and displays the Top-3 most similar popular books. This provides an additional recommendation option that might not appear in the pure CBF Top-N if the input book comes from a different cluster.

**Example of Top-3 Popular Recommendations (for input 'bali'/'bliss' from Cluster 0):**

| Rank | Title                        | Authors         | Categories   | Published Year | Content Similarity |
| :--- | :--------------------------- | :-------------- | :----------- | :------------- | :----------------- |
| 1    | the alchemist                | paulo coelho    | fiction      | 2006           | 0.158              |
| 2    | the giver                    | lois lowry      | juvenile fiction | 2006           | 0.151              |
| 3    | the fellowship of the ring | j r r tolkien | fiction      | 2003           | 0.151              |

**Advantages of the CBF + K-Means Approach:**

*   **Potential for Increased Diversity/Serendipity:** By suggesting popular items from other clusters (even if their content similarity is lower than the pure CBF recommendations), the system can help users discover items outside their "filter bubble."
*   **Leverages Data Structure:** Uses implicit information from user interactions (ratings, page/rating counts) through clustering to inform recommendations.
*   **Provides Additional Context:** The cluster information ("Underrated", "Best Seller") gives additional context to the recommended books.

**Disadvantages of the CBF + K-Means Approach:**

*   **Dependency on Cluster Quality:** The effectiveness of the additional recommendations heavily depends on how good and meaningful the K-Means clustering results are. If the clusters are not well-separated or do not represent a useful concept (like popularity), the benefit is diminished.
*   **Additional Complexity:** Requires extra steps for clustering and cluster interpretation.
*   **Still Content-Based at its Core:** The "popular" recommendations are still sorted by content similarity (CBF) with the input, just filtered from a specific cluster. This is not a pure collaborative approach.
*   **Cluster Imbalance:** As seen in the evaluation, if one cluster is highly dominant (Cluster 0: 99.7%), the ability to recommend items from the minority cluster (Cluster 1: 0.3%) becomes limited or less impactful.

## Evaluation

In this section, an evaluation of the developed recommendation system models is conducted: pure Content-Based Filtering (CBF) and K-Means Clustering used to enrich the recommendations. The evaluation aims to measure the relevance, diversity, and quality of the data structures found by the models.

The evaluation metrics used are tailored to the task of each model:

1.  **Evaluation of Content-Based Filtering (CBF):**
    *   Similarity Score (Cosine Similarity - as a proxy for Relevance)
    *   Intra-List Similarity (as a metric for Diversity)
2.  **Evaluation of K-Means Clustering:**
    *   Silhouette Score
    *   Calinski-Harabasz Index
    *   Davies-Bouldin Index
3.  **Evaluation of the Hybrid Model (CBF + K-Means):**
    *   Cluster Alignment Analysis

### Evaluation of Content-Based Filtering (CBF)

The following metrics are used to evaluate the recommendations generated by the pure CBF model (TF-IDF & Cosine Similarity).

#### 1. Similarity Score (Relevance)

*   **Metric:** Average & Highest Similarity Score.
*   **Purpose:** To measure how similar (relevant) the recommended books are to the input book based on their content.
*   **How it Works:** This metric uses the Cosine Similarity scores generated during the modeling stage.
    *   `Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||)`
    *   Scores range from 0 (not similar) to 1 (identical). A higher score for the top recommendations indicates better content relevance. The average score gives a general idea of the similarity of the recommendation list, while the highest score shows the most similar item.
*   **Project Results:**
    *   For input 'Gilead', Average Score: 0.31, Highest Score: 0.32.
    *   For input 'The Four Loves', Average Score: 0.49, Highest Score: 0.64.
    *   For input 'Rage of Angels', Average Score: 0.48, Highest Score: 0.51.
    *   For input 'The One Tree', Average Score: 0.41, Highest Score: 0.48.
    *   For input '1984', Average Score: 0.50, Highest Score: 0.63.
*   **Interpretation:** The average and highest similarity scores indicate a moderate to fairly good level of relevance. The recommendations provided have a clear content relationship with the input book, but are not overly identical, which might be desirable for discovery.

#### 2. Intra-List Similarity (Diversity)

*   **Metric:** Average Intra-List Similarity.
*   **Purpose:** To measure how similar the books *within* a recommendation list are to each other. A lower score indicates higher diversity (the recommended books are not too similar to one another).
*   **How it Works:** This metric calculates the average Cosine Similarity for all unique pairs of books in the Top-N recommendation list. A score of 0 means no similarity at all between recommendations (very diverse), a score of 1 means all recommendations are identical (not diverse). Calculated using the `calculate_cbf_diversity` function.
    *   Concept: `Avg(CosineSim(Item_i, Item_j))` for all `i != j` in the recommendation list.
*   **Project Results:**
    *   For input 'Gilead': 0.34
    *   For input 'The Four Loves': 0.47
    *   For input 'Rage of Angels': 0.32
    *   For input 'The One Tree': 0.20
    *   For input '1984': 0.35
*   **Interpretation:** The resulting Intra-List Similarity values are relatively low (well below 0.7), indicating that the recommendations generated by the CBF model have **good diversity**. The system does not just suggest books that are very similar to each other.

### Evaluation of K-Means Clustering

The following metrics are used to assess the quality of the clustering of book data into 2 clusters using K-Means, before these clusters are used in the hybrid recommendation. The choice of two clusters (k=2) was based on practical considerations for ease of interpretation in the recommendation system. With two groups, the clustering results can be more easily labeled and understood in meaningful categories for recommendations, such as distinguishing between 'popular/best-seller' and 'underrated/niche' books. This evaluation is important because the quality of the additional recommendations depends on the quality of the clusters formed.

#### 1. Silhouette Score

*   **Purpose:** To measure how well each object (book) fits into its own cluster compared to the nearest neighboring cluster.
*   **How it Works:** The score ranges from -1 to 1.
    *   A value close to +1: The object is well-matched to its own cluster and far from other clusters.
    *   A value around 0: The object is close to the boundary between clusters.
    *   A value close to -1: The object may have been misclassified into a cluster.
    *   The formula compares the average distance of an object to other points in its cluster (a) with the average distance of the object to points in the next nearest cluster (b): `(b - a) / max(a, b)`. The overall score is the average of the Silhouette scores for all objects.
*   **Project Result:** 0.976.
*   **Interpretation:** A very high score (close to 1) indicates that K-Means successfully created **very dense and well-separated clusters**. The books within a single cluster are very similar to each other (based on the clustering features) and very different from the books in the other cluster.

#### 2. Calinski-Harabasz Index (Variance Ratio Criterion)

*   **Purpose:** To measure the ratio of the variance between clusters (how far apart the cluster centers are) to the variance within clusters (how dense the data points are within a cluster).
*   **How it Works:** A higher score indicates better clusters (denser and more separated). There is no upper limit, but a relatively higher value is better.
    *   Formula: `(SSB / SSW) * ((N - k) / (k - 1))` where SSB is the Sum of Squares Between clusters, SSW is the Sum of Squares Within clusters, N is the number of data points, and k is the number of clusters.
*   **Project Result:** 10063.465.
*   **Interpretation:** This very high value indicates that the **cluster structure found is very clear**, with the variance between clusters being much larger than the variance within clusters.

#### 3. Davies-Bouldin Index

*   **Purpose:** To measure the average 'similarity' between each cluster and its most similar cluster, where similarity is the ratio of the intra-cluster distance to the inter-cluster distance.
*   **How it Works:** A lower score indicates better cluster separation, with 0 being the lowest possible score. The index calculates the ratio of the spread within a cluster to the separation between clusters for each cluster, then averages them.
    *   Formula: `(1/k) * Σ max( (Si + Sj) / Dij )` where k is the number of clusters, Si is the average deviation of cluster i from its centroid, and Dij is the distance between the centroids of clusters i and j. The maximum ratio is found for each cluster i against another cluster j.
*   **Project Result:** 0.353.
*   **Interpretation:** This relatively low score (close to 0) also indicates that the **clusters are well-separated**.

**Conclusion of Clustering Evaluation:** All three metrics (Silhouette, Calinski-Harabasz, Davies-Bouldin) consistently show that the K-Means algorithm with k=2 successfully found a strong and clear cluster structure in the data based on the `average_rating`, `num_pages`, and `ratings_count` features. This provides a good foundation for using the cluster labels in the hybrid recommendation approach.

### Evaluation of the Hybrid Model (CBF + K-Means)

This metric looks at how the pure CBF recommendations interact with the found cluster structure.

#### 1. Cluster Alignment

*   **Purpose:** To analyze which cluster the CBF recommendations come from, relative to the cluster of the input book.
*   **How it Works:** For an input book from a specific cluster, the percentage of Top-N CBF recommendations that come from the same cluster is calculated. This is computed using the `analyze_cluster_alignment` function.
*   **Project Results:**
    *   For an input book from Cluster 0 ("Underrated"): 100% (5/5) of the recommendations came from Cluster 0.
    *   For an input book from Cluster 1 ("Best Seller"): 0% (0/5) of the recommendations came from Cluster 1 (all came from Cluster 0).
*   **Interpretation:** This result shows that the CBF recommendations are heavily influenced by the input book's origin cluster, especially the dominant cluster (Cluster 0). When the input comes from the minority cluster (Cluster 1), pure CBF still tends to recommend books from the majority cluster (Cluster 0) because it is more likely to have more content-wise near neighbors there. This highlights the potential benefit of the `recommend_with_cluster_info` function, which explicitly presents popular book recommendations from Cluster 1 as an addition, even if their content similarity might be lower.

## References

1.  Linden, G., Smith, B., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. *IEEE Internet Computing*, 7(1), 76-80. Available: [link.](https://ieeexplore.ieee.org/document/1167344)
2.  Smith, B., & Linden, G. (2017). Two decades of recommender systems at Amazon.com. *IEEE Internet Computing*, 21(3), 12-18.
3.  Martinez, M. (2017). Amazon: Everything you wanted to know about its algorithm and innovation. *IEEE Computer Society Tech News*. Available: [link.](https://www.computer.org/publications/tech-news/trends/amazon-all-the-research-you-need%20about-its-algorithm-and-innovation)
4.  Gomez-Uribe, A., & Neil, N. (2015). The Netflix Recommender System: Algorithms, Business Value, and Innovation. *ACM Transactions on Management Information Systems*, 6(4), 1-19. Available: [link.](https://dl.acm.org/doi/10.1145/2843948)
5.  Isinkaye, F. O., Folajimi, Y. O., & Ojokoh, B. (2015). Recommendation systems: Principles, methods and evaluation. *Egyptian Informatics Journal*, 16(3), 261-273. Available: [link.](https://www.researchgate.net/publication/282860285_Recommendation_systems_Principles_methods_and_evaluation)
6.  Khusro, S., Ali, Z., & Ullah, I. (2016). Recommender Systems: Issues, Challenges, and Research Opportunities. *In Information Science and Applications (ICISA), Ho Chi Minh*.
7.  Azizi, M., & Do, H. (2018). A Collaborative Filtering Recommender System for Test Case Prioritization in Web Applications. *In Proceedings of SAC 2018: Symposium on Applied Computing, Pau*.

---

## Authors
-   I Dewa Gede Mahesta Parawangsa - [your.email@example.com](mailto:your.email@example.com)

## Version History
*   **0.1**
    *   Initial Release: Includes data preparation, EDA, Content-Based Filtering model, K-Means clustering, and model evaluation.

## License
This project is licensed under the MIT License - see the LICENSE.md file for details.
