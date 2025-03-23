<div align="center">
  <img src="https://raw.githubusercontent.com/alouanemed/NoSQL-Movie/main/assets/movie_recommendation_banner.png" alt="Movie Recommendation System with MongoDB" width="600">
  <h1><samp>🎬 Builf a Simepl a Movie Recommendation System with MongoDB</samp></h1>
  <p>
    <samp>Harnessing the flexibility of NoSQL and the power of collaborative filtering to suggest your next favorite film.</samp>
  </p>
</div>

<br>

<div align="center">
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT">
  </a>
  <img src="https://img.shields.io/badge/Language-Python-blue.svg" alt="Language: Python">
  <img src="https://img.shields.io/badge/Database-MongoDB-green.svg" alt="Database: MongoDB">
  <img src="https://img.shields.io/badge/Framework-Collaborative Filtering-orange.svg" alt="Framework: Collaborative Filtering">
</div>

<br>

## <samp>📜 Project Overview</samp>

In today's digital age, where users are overwhelmed with choices, recommendation systems have become indispensable for discovering relevant and personalized content. This capstone project focuses on the design and implementation of a movie recommendation system utilizing **User-Based Collaborative Filtering** and the flexible, scalable NoSQL database, **MongoDB**.

The primary goal is to demonstrate how MongoDB can effectively manage user and movie data, and how Python tools like Pandas and scikit-learn can be employed to analyze this data and generate tailored movie recommendations. This project report, undertaken as part of the **Licence d’excellence, Systèmes d’Information et Intelligence Artificielle (SIIA)** program, details the entire process from database modeling to system implementation and evaluation.

## <samp>✨ Key Features</samp>

* **Movie Recommendation Engine:** Provides personalized movie suggestions based on user preferences and the ratings of similar users.
* **MongoDB Integration:** Leverages MongoDB's document-oriented structure for efficient storage and retrieval of user and movie data.
* **User-Based Collaborative Filtering:** Implements a collaborative filtering algorithm that identifies users with similar tastes to generate recommendations.
* **Flexible Data Modeling:** Showcases the adaptability of MongoDB schemas for handling diverse user and movie information.
* **Python Implementation:** Utilizes Python along with libraries like Pandas, scikit-learn, and pymongo for data manipulation, algorithm implementation, and database interaction.
* **Jupyter Notebook Demonstration:** The project includes a Jupyter Notebook for easy testing, demonstration, and visualization of the recommendation process.

## <samp>🗺️ Table of Contents</samp>

* [📜 Project Overview](#-project-overview)
* [✨ Key Features](#-key-features)
* [🗺️ Table of Contents](#️-table-of-contents)
* [🚀 Getting Started](#-getting-started)
    * [Prerequisites](#prerequisites)
    * [Setup](#setup)
* [💾 Database Modeling in MongoDB](#-database-modeling-in-mongodb)
    * [Schemas](#schemas)
    * [Indexing Strategy](#indexing-strategy)
* [🧠 Movie Recommendation System](#-movie-recommendation-system)
    * [Collaborative Filtering: User-Based vs. Item-Based](#collaborative-filtering-user-based-vs-item-based)
    * [Proposed Approach](#proposed-approach)
* [🛠️ Implementation](#️-implementation)
* [📊 Conclusion](#-conclusion)
    * [Strengths](#strengths)
    * [Limitations](#limitations)
    * [Recommendations](#recommendations)
* [🔗 Annex](#-annex)
* [📄 License](#-license)
* [🙏 Acknowledgements](#-acknowledgements)

## <samp>🚀 Getting Started</samp>

Ready to explore the world of personalized movie recommendations? Follow these steps to understand and potentially run the project.

### <samp>Prerequisites</samp>

Ensure you have the following installed and configured:

* **Python 3.x:** The primary programming language used for this project.
* **MongoDB:** A running instance of MongoDB to store the user and movie data.
* **pip:** Python package installer to install the necessary libraries.
* **Required Python Libraries:** Install the following libraries using pip:
    ```bash
    pip install pymongo pandas scikit-learn
    ```
* **Jupyter Notebook (Optional):** Recommended for running and exploring the provided demonstration notebook.

### <samp>Setup</samp>

1.  **Clone the Repository:**
    ```bash
    git clone <repository_url> # Replace with the actual repository URL
    cd <repository_directory>
    ```
2.  **MongoDB Setup:** Ensure your MongoDB server is running. You might need to import initial data if the repository doesn't include a data seeding script.
3.  **Review Jupyter Notebook:** Open and review the Jupyter Notebook (if provided in the repository) to understand the data seeding process, database interactions, and the recommendation algorithm.

## <samp>💾 Database Modeling in MongoDB</samp>

The project utilizes MongoDB to store information about users and movies. The database consists of two main collections: `users` and `movies`.

### <samp>Schemas</samp>

* **`users` Collection:** Stores user profiles and their movie rating history.
    ```json
    {
      "_id": "user_001",
      "username": "Mohamed",
      "email": "mo@usms.ac.ma∂",
      "preferences": {
        "genres": ["Action", "SF"],
        "actors": ["Tom Hanks", "Charlize Theron"]
      },
      "history": [
        {
          "movie_id": "The God father",
          "rating": 5,
          "watched_on": "2025-01-01T20:00:00Z"
        },
        {
          "movie_id": "The Shawshank Redemption",
          "rating": 3,
          "watched_on": "2025-01-05T19:00:00Z"
        }
      ]
    }
    ```

* **`movies` Collection:** Stores metadata about movies.
    ```json
    {
      "_id": "movie_int_001",
      "title": "The Matrix",
      "genres": ["Action", "SF"],
      "actors": ["Keanu Reeves", "Carrie-Anne Moss"],
      "description": "Dans un futur dystopique...",
      "release_date": "1999-03-31"
    }
    ```

### <samp>Indexing Strategy</samp>

The following indexing strategy is employed for efficient data retrieval:

| Field                 | Index Type     | Justification                                                                 |
| --------------------- | -------------- | --------------------------------------------------------------------------- |
| `_id` (default)       | Primary Index  | Enables direct access by unique identifier (automatically created by MongoDB). |
| `title` (movies)      | Text Index     | Facilitates text-based search to quickly find movies by title.             |
| `history.movie_id` (users) | (Multi-key) Index (if needed) | Useful for reverse lookups, e.g., finding which users have watched a specific movie. |

## <samp>🧠 Movie Recommendation System</samp>

The core of this project is the implementation of a **User-Based Collaborative Filtering** recommendation system.

### <samp>Collaborative Filtering: User-Based vs. Item-Based</samp>

Collaborative filtering is a widely used technique that relies on the idea that users who have liked similar items in the past are likely to have similar preferences in the future. There are two main types:

* **User-Based Collaborative Filtering:** Compares users to each other to find similar "neighbors." Recommendations for a target user are then generated based on the items that their neighbors liked but the target user has not yet seen.
* **Item-Based Collaborative Filtering:** Compares items to each other based on user ratings. When a user interacts with an item, the system recommends other items that are similar to it.

This project utilizes **User-Based Collaborative Filtering** due to its simplicity and effectiveness, especially when the number of movies is moderate.

### <samp>Proposed Approach</samp>

The recommendation process involves the following steps:

1.  **Collect Ratings:** Users provide ratings (e.g., on a scale of 1 to 5) for the movies they have watched. These ratings are stored in the `history` field of the `users` collection in MongoDB.
2.  **Construct User-Item Matrix:** A user-item matrix is created where rows represent users and columns represent movies. The value in each cell is the rating given by the user to the movie (or 0/NaN if no rating exists).
3.  **Measure Similarity:** The similarity between users is calculated using a metric like **cosine similarity**. This project leverages the `cosine_similarity` function from the `sklearn.metrics.pairwise` module in scikit-learn.
4.  **Generate Recommendations:** For a target user, the system identifies the most similar users (neighbors). It then looks at the movies that these neighbors have highly rated (e.g., rating >= 4) but the target user has not yet seen. These movies are then proposed as recommendations.

## <samp>🛠️ Implementation</samp>

The implementation of this movie recommendation system was primarily done using a **Jupyter Notebook**. The environment included:

* A local instance of **MongoDB** for data storage.
* **Python 3** with the necessary libraries installed (pymongo, pandas, scikit-learn).

The Jupyter Notebook likely contained scripts to:

* **Seed Data:** Insert initial movie and user data with some sample ratings into the MongoDB database.
* **Display Database Content:** Show the contents of the `users` and `movies` collections.
* **Build User-Item Matrix:** Transform the rating data into a Pandas DataFrame representing the user-item matrix.
* **Run Recommendation Algorithm:** Implement the cosine similarity calculation and the logic for generating movie recommendations for a given user.
* **Visualize Results:** Display the generated movie recommendations.

The report also mentions a function `rate_movie(user_id, movie_id, rating)` to simulate adding new ratings to the database and observing how it affects future recommendations.

## <samp>📊 Conclusion</samp>

This project successfully demonstrated the creation of a movie recommendation system based on User-Based Collaborative Filtering using MongoDB for data storage and Python tools for analysis and algorithm implementation.

### <samp>Strengths</samp>

* MongoDB's flexible document structure effectively handled complex user data and varying movie information.
* The system can scale as the number of users and movies grows, thanks to MongoDB's scalability features.
* The Jupyter Notebook environment provides a clear and easy-to-understand demonstration of the system's functionality.

### <samp>Limitations</samp>

* The system may struggle to provide recommendations for new users with no rating history (the "cold start" problem).
* Highly popular movies might dominate recommendations, potentially overshadowing less popular but relevant titles.
* The accuracy of recommendations depends on the availability and quality of user ratings. Sparsity in the user-item matrix can impact the effectiveness of the collaborative filtering approach.

### <samp>Recommendations</samp>

* Consider integrating a web framework like Flask to expose the recommendation system as a REST API for broader usability.
* Combine Collaborative Filtering with content-based filtering techniques (using movie genres, actors, etc.) to address the cold start problem.
* Implement optimizations for handling larger datasets, such as using sparse matrices or caching mechanisms.

## <samp>🙏 Acknowledgements</samp>

This project was undertaken as part of the USMS's Informaiton System and AI program under the guidance of **Prof. Khoudrifi**.

  
