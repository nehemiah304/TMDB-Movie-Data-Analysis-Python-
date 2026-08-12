# TMDB-Movie-Data-Analysis-Python-
This project analyzed a dataset of movies from The Movie Database (TMDB), covering titles, budgets, revenue, popularity scores, genres, directors, release dates, and vote averages. The goal was to uncover patterns in what drives a movie's commercial and audience success, using Python for the full analysis pipeline.

 ## 🔍 Overview :
This project performs exploratory data analysis (EDA) on TMDB movie data using Python. Ten analytical questions were developed to uncover what drives a movie's commercial and audience success — from blockbuster revenue and profitability to genre economics, director output, and the relationship between popularity and rating.

The goal is to surface patterns that explain why certain movies dominate box-office and popularity charts, and to build a clean, defensible dataset that separates "unknown" financial data from genuinely low-budget/low-revenue films.

📌 Objectives

Load and inspect the TMDB dataset to understand its structure and quality
Clean the data: drop unused columns, remove duplicates, fix data types, handle missing values
Build a dedicated financial subset to avoid unrecorded budget/revenue values skewing money-based questions
Split multi-genre entries into individual rows for genre-level analysis
Answer 10 business questions covering popularity, revenue, profitability, genres, output trends, directors, runtime, and rating
Summarize findings into clear, actionable takeaways

❓ Business Questions

Which movies were the most popular?
Which movies earned the most revenue?
Which movies were the most profitable?
Does spending a bigger budget lead to more revenue?
What are the most common movie genres?
Which genres bring in the most average revenue?
How has the number of movies released changed over the years?
Which directors have the most movies in this dataset?
What's the typical movie runtime?
Is a movie's popularity related to how well it's rated (vote average)?

📚 Dataset Description Source: TMDB movie dataset (tmdb__1_.xlsx) — 10,869 records, 21 columns. Columns retained after cleaning: id, popularity, budget, revenue, original_title, cast, director, runtime, genres, release_date, vote_count, vote_average, release_year, budget_adj, revenue_adj. Columns dropped: homepage, tagline, overview, keywords, imdb_id, production_companies — not needed for this analysis.

🛠 Tools & Technologies Used

Python
Pandas — data loading, cleaning, aggregation
NumPy — numerical operations
Matplotlib & Seaborn — visualization

🧹 Data Cleaning and Preparation

Dropped six unused columns (homepage, tagline, overview, keywords, imdb_id, production_companies), reducing the dataset from 21 to 15 columns.
Removed duplicate rows and dropped a handful of rows missing an id (blank/junk records) — dataset settled at 10,865 clean rows.
Converted release_date to proper datetime and release_year to a whole-number (Int64) type.
Filled missing values in director, cast, and genres with "Unknown" so groupby and value_counts operations run cleanly without dropping rows.
Built a separate money_df filtered to budget > 0 and revenue > 0 (3,854 of 10,865 movies), since zero values in these fields mean "not recorded," not "free movie." A profit column (revenue − budget) was added to this subset. All money-based questions (Q2–Q4) draw from this filtered dataset rather than the full one, to avoid unrecorded values distorting results.
Split the pipe-separated genres field (e.g. "Action|Adventure") into individual rows via explode(), expanding the dataset to 26,978 genre-level rows for genre analysis (Q5–Q6).

📈 Key Findings

Most Popular Movies: Jurassic World tops the list (popularity score 32.99), followed by Mad Max: Fury Road (28.42) and Interstellar (24.95) — all from the mid-2010s, reflecting how the popularity metric skews toward recent releases.
Highest-Grossing Movies: Avatar leads with $2.78B in revenue, ahead of Star Wars: The Force Awakens ($2.07B) and Titanic ($1.85B).
Most Profitable Movies: Avatar again leads on profit, with Star Wars: The Force Awakens and Titanic close behind — the same handful of blockbusters dominate both revenue and profit rankings.
Budget vs. Revenue Correlation: 0.69 — a moderately strong positive relationship. Bigger budgets tend to earn more, but the correlation isn't strong enough to guarantee it; plenty of low-budget films outperform expensive ones.
Most Common Genres: Drama (4,760 movies), Comedy (3,793), and Thriller (2,907) are the three most frequent genres in the dataset.
Highest-Earning Genres (by average revenue): Animation leads at $257.1M average revenue per movie, ahead of Adventure ($218.3M) and Fantasy ($218.2M) — notably, none of the three most common genres (Drama, Comedy, Thriller) crack the top of the revenue ranking.
Movies Released Per Year: Output trends upward over time, consistent with the film industry's overall growth in volume.
Most Prolific Directors: Woody Allen leads with 45 movies in the dataset, followed by Clint Eastwood (34), and a tie between Steven Spielberg and Martin Scorsese (29 each).
Typical Runtime: Median runtime is 99 minutes (mean 102.1 minutes), with the middle 50% of movies (25th–75th percentile) running 90–111 minutes.
Popularity vs. Rating Correlation: 0.21 — a weak relationship. A highly-rated movie isn't necessarily a popular one, and vice versa.

📊 Business Insights

🎬 A small set of blockbusters dominates every top-line chart. Avatar, Star Wars: The Force Awakens, and Titanic repeatedly appear across the revenue and profit rankings, while Jurassic World and Mad Max: Fury Road dominate popularity. This concentration suggests that box-office success is driven by a small number of tentpole releases rather than being evenly distributed across the industry — a pattern that matters for any business trying to model expected returns from a "typical" release.

💰 Budget buys revenue, but only loosely. The 0.69 correlation between budget and revenue confirms a real relationship, but it's far from deterministic (a correlation of 1.0 would mean budget fully predicts revenue). This means high-budget productions carry real financial risk — a big spend narrows the odds of failure but doesn't eliminate them, and the data shows real examples of low-budget films outperforming expensive ones.

🎭 The genres people watch most aren't the genres that earn the most per film. Drama, Comedy, and Thriller are the most frequently produced genres by volume, but Animation, Adventure, and Fantasy generate the highest average revenue per movie. This gap between production volume and per-title earning power suggests the industry may be over-indexed on genres that are reliable to produce but under-indexed on genres that are more lucrative on a per-project basis.

🎥 Popularity and quality are only weakly linked. At 0.21 correlation, audience rating explains very little of what makes a movie "popular" in this dataset's metric. This implies popularity is driven more by marketing reach, franchise recognition, or release timing than by how well-reviewed a film is — a distinction worth keeping in mind for any recommendation or marketing strategy built on this data.

📉 Notable Trends

Movie output has grown steadily over time, consistent with the industry's expansion in both production volume and distribution reach.
Runtime is tightly clustered: half of all movies run between 90 and 111 minutes, suggesting a strong industry convention around feature-length pacing.
The financial dataset is a small fraction of the whole (3,854 of 10,865 movies, ~35%) — the majority of records have unrecorded budget/revenue, a data-quality reality that shaped the decision to analyze money questions on a separate, filtered subset rather than the full dataset.
A small group of directors (led by Woody Allen at 45 films) account for a disproportionate share of prolific output, pointing to a core of highly active filmmakers within the dataset's time span.

💡 Recommendations

Treat budget as a risk-reducer, not a revenue guarantee, when evaluating production decisions — the 0.69 correlation supports investment but doesn't justify assuming a linear payoff.
Prioritize genre strategy around per-title earning power (Animation, Adventure, Fantasy) rather than production volume alone (Drama, Comedy, Thriller), especially where budget is constrained.
Don't use popularity scores as a proxy for quality (or vice versa) in downstream modeling or recommendation work — the weak 0.21 correlation means they capture different signals and should be evaluated separately.
Flag the ~65% of records with unrecorded budget/revenue as a data-collection gap worth addressing if this analysis is extended — the financial insights here are only as strong as the 3,854-movie subset they're built on.
