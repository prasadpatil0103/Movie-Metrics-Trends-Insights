# 📊 Movie Metrics: Trends & Insights

**Author:** Prasad Patil  
**Institution:** Syracuse University - School of Information Studies  
**Date:** April 17, 2025

---

## 📖 Table of Contents
- [Introduction](#introduction)
- [Data Sources](#data-sources)
- [Data Exploration and Cleaning](#data-exploration-and-cleaning)
- [Research Questions](#research-questions)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Key Stages of Implementation](#key-stages-of-implementation)
- [Output Files](#output-files)
- [Key Findings](#key-findings)
- [Future Work](#future-work)

---

## 📝 Introduction

This project presents an exploratory analysis of movie ratings, focusing on critic and audience scores across different genres, years, and cast groupings. The project integrates structured and semi-structured data sources, cleans and merges them, and derives meaningful visual and statistical insights.

**Objective:** To uncover patterns in movie evaluations and understand the influence of various factors on critical and public reception.

---

## 📁 Data Sources

### Input Files

#### **movies.csv** (Structured Data)
Contains metadata for **1,153 movies**, including:
- Movie title
- Release year
- Genres (multiple genres per movie)
- Cast information

#### **movie_info.json** (Semi-Structured Data)
Scraped from Rotten Tomatoes, providing:
- Critic scores
- Audience scores
- Release dates
- URLs

### Output Files

The analysis generates three aggregated datasets:

- **Scores_by_Genre.csv** - Average scores by genre
- **Scores_By_Year.csv** - Average scores by year
- **Cast_group_vs_scores.csv** - Scores grouped by cast popularity

The integration of structured (`.csv`) and semi-structured (`.json`) sources enables a richer exploration of patterns in movie ratings.

---

## 🧹 Data Exploration and Cleaning

To prepare the data for analysis, several key steps were taken:

1. **Parsing and Conversion**: The scores from the JSON dataset, initially stored as strings with `%` symbols, were cleaned and converted to numeric format.

2. **Handling Missing Values**: Rows with missing or invalid scores were dropped.

3. **Genre Explosion**: As many movies belonged to multiple genres, the genre column was exploded, resulting in one row per genre per movie.

4. **Datetime Formatting**: The release dates were parsed into proper datetime objects and then simplified to extract only the year for trend analysis.

5. **Data Deduplication**: Duplicate entries based on movie titles and URLs were removed.

6. **Unit Change**: Runtime values (if used) were converted from minutes to hours for better interpretability.

7. **Elimination of Non-Essential Columns**: Columns like `href`, `thumbnail`, `thumbnail_width`, and `thumbnail_height` were removed from the movies_df dataset to reduce noise and improve processing efficiency.

---

## 🔍 Research Questions

### 1. Which Genre Has the Highest Ratings?

**Analysis Method:**
- Exploded the genre column in the `movies.csv` dataset
- Calculated average scores for each genre
- Joined with parsed critic and audience scores from `movie_info.json`

**Insights:**
- **Documentaries and Dramas** consistently received the highest critic scores
- Genres like **Comedy and Action**, while not leading in critic scores, fared better with audience ratings
- There's a noticeable gap between critic and audience preferences for genres like **Horror and Sci-Fi**, suggesting critics may judge these genres more harshly than general viewers

### 2. How Have Scores Changed Over the Years?

**Analysis Method:**
- Extracted year from release date field
- Grouped movies by year
- Computed average scores per year

**Insights:**
- **Critic scores** have remained relatively stable, with slight variations over the years
- **Audience scores** show more fluctuation, possibly influenced by evolving cultural preferences, changes in movie production styles, or the impact of social media and online reviews
- A **growing gap** between critic and audience scores in recent years may reflect a divergence in taste or the rise of fan-driven hype around certain films

### 3. Do Popular Casts Influence Ratings?

**Analysis Method:**
- Grouped data by cast size/popularity (Small, Medium, Large)
- Averaged critic and audience scores within these groups

**Insights:**
- Movies with **medium-sized casts** performed best with both critics and audiences
- Surprisingly, movies with **large casts** did not outperform smaller productions, indicating that star power alone does not guarantee better ratings
- This suggests that while a known cast may attract initial attention, the **overall content quality and storytelling** are more influential on critical reception

---

## 🛠️ Technologies Used

### Programming Language
- **Python 3.x**

### Development Environment
- **Jupyter Notebook**

### Libraries
- **pandas** - Data manipulation and analysis
- **json** - Parsing semi-structured data
- **matplotlib** - Data visualization
- **seaborn** - Statistical data visualization

---

## 💻 Installation

### Prerequisites
- Python 3.x installed on your system
- pip package manager

### Setup Instructions
```bash
# Clone the repository (if applicable)
git clone [your-repository-url]
cd movie-metrics-analysis

# Install required packages
pip install pandas matplotlib seaborn jupyter

# Or use requirements.txt if provided
pip install -r requirements.txt
```

---

## 🚀 Usage

1. **Ensure data files are in place:**
   - `movies.csv`
   - `movie_info.json`

2. **Launch Jupyter Notebook:**
```bash
   jupyter notebook
```

3. **Open the analysis notebook** and run all cells sequentially

4. **Review outputs:**
   - Generated CSV files with aggregated results
   - Visualization plots (PNG images)

---

## 📋 Key Stages of Implementation

### Stage 1: Data Loading
- Read structured data from `movies.csv` and `Scores_by_*` CSV files
- Parse semi-structured JSON data (`movie_info.json`) containing critic and audience scores

### Stage 2: Data Cleaning and Preprocessing
- Percentage strings in the JSON scores were stripped and converted to numerical format
- Missing or incomplete entries were removed
- Genres were exploded to allow genre-wise analysis
- The `release_date` field was parsed to extract the release year
- Duplicate entries were dropped
- Irrelevant columns like `href`, `thumbnail`, `thumbnail_width`, and `thumbnail_height` were removed from the movies DataFrame

### Stage 3: Data Transformation
- Data was grouped and aggregated using `groupby()` operations
- Calculated average critic and audience scores by genre, year, and cast group

### Stage 4: Visualization
The script generates multiple visual outputs using `matplotlib`:
- Bar plots comparing genre-wise average scores
- Line plots showing score trends over years
- Bar charts comparing cast group ratings

### Stage 5: Data Export
- Aggregated results were exported to new CSV files for easy reference and reporting

---

## 📤 Output Files

### 1. Scores_by_Genre.csv
Contains the average critic and audience scores for each individual genre. By exploding multi-genre entries and aggregating scores, this dataset provides a clear view of how different genres are rated, enabling genre-level comparisons and trends.

### 2. Scores_By_Year.csv
Presents a year-wise breakdown of average critic and audience scores. Derived from parsing release dates and grouping the data by year. Instrumental in identifying temporal trends, such as shifts in audience preferences or critical standards over time.

### 3. Cast_group_vs_scores.csv
Categorizes movies based on cast group size (Small, Medium, or Large) and computes average scores within each category. Helps assess the impact of cast popularity or ensemble size on a movie's reception, offering insights into whether star power influences ratings.

These output files serve as concise summaries of the core analysis and are well-suited for downstream use in dashboards, visualizations, or external reporting.

---

## 💡 Key Findings

### Genre Preferences
✅ Documentaries and Dramas receive highest critical acclaim  
✅ Comedy and Action resonate better with general audiences  
✅ Critics judge Horror and Sci-Fi more harshly than viewers

### Temporal Trends
✅ Critic standards remain relatively stable over time  
✅ Audience preferences show more volatility and change  
✅ Growing divergence between critics and audiences in recent years

### Cast Impact
✅ Medium-sized casts perform best overall  
✅ Large star-studded casts don't guarantee better ratings  
✅ **Content quality > Star power** for both critics and audiences

---

## 🔮 Future Work

This analysis could be extended with:

- **IMDb scores** for cross-platform comparison
- **Box office performance** correlation analysis
- **Sentiment analysis** from reviews or social media
- **Budget and production value** impact studies
- **Regional variations** in ratings across different markets
- **Director and writer influence** on ratings
- **Streaming vs. theatrical release** comparison

---

## 📂 Project Structure
```
movie-metrics-analysis/
│
├── movies.csv                      # Input: Movie metadata
├── movie_info.json                 # Input: Rotten Tomatoes scores
├── analysis_notebook.ipynb         # Main Jupyter notebook
│
├── Scores_by_Genre.csv            # Output: Genre analysis
├── Scores_By_Year.csv             # Output: Temporal analysis
├── Cast_group_vs_scores.csv       # Output: Cast analysis
│
├── genre_scores.png               # Visualization
├── year_trends.png                # Visualization
├── cast_group_scores.png          # Visualization
│
└── README.md                      # This file
```

---

## 🎯 Conclusion

This analysis provided a comprehensive look at how **genre**, **release year**, and **cast group** affect movie ratings. By merging multiple sources and applying consistent cleaning and analysis techniques, we were able to extract actionable insights and confirm that while star casts help, **content and execution matter more**.

The methodology is designed for **reproducibility and modularity**, enabling easy extensions or updates to the dataset.

---

## 📧 Contact

**Prasad Patil**  
Syracuse University - School of Information Studies

For questions or collaborations, please reach out via the university email system.

---

## 📄 License

[Specify your license here - e.g., MIT, Apache 2.0, etc.]

---

*Report generated on November 15, 2025*
