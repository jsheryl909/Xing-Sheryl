Exploring Movie Ratings and Film Attributes Using MovieLens and TMDB Metadata

-------------------------------------------------------------------------------------------------------------------------------------

Contributors

Sheryl John

Xing Huang

------------------------------------------------------------------------------------------------------------------------------------
Summary

This project examines how movie features relate to user ratings by combining the MovieLens ratings dataset with descriptive movie information from the TMDB based Movies Metadata collection. The goal is to see whether certain types of movies tend to receive higher or lower ratings and to understand how attributes such as genre, release year, and runtime appear to influence user preferences. Once the datasets were combined and cleaned, we explored trends and built a simple recommendation approach based on the patterns we observed.

We selected MovieLens because it is widely trusted for research and is designed to protect user privacy. It contains about 100,000 ratings from roughly 600 users on many different films. We paired it with the Movies Metadata dataset because it provides rich descriptive information, including genres and release dates. Since the two datasets come from different sources, the project required several steps to standardize fields, match identifiers, check licensing, and validate that the data could be used for academic analysis.

Our work followed the order of the data lifecycle presented in class. We began by collecting both datasets, reviewing their terms of use, and organizing the files in a consistent directory structure. In the cleaning stage, we standardized IDs, converted timestamps, extracted release years, fixed formatting issues, and removed records that lacked essential information. We then merged the datasets by matching the MovieLens movieId field with the TMDB id field. The combined dataset allowed us to study how the characteristics of movies relate to the ratings that users give them.

During exploratory analysis, we looked at rating distributions, average ratings per genre, trends across release years, and the relationship between runtime and user sentiment. Our results showed clear patterns. Genres such as drama, history, and documentary usually received higher average ratings. Movies from earlier decades tended to have slightly higher averages, although more recent films showed a wider spread of values. Runtime did not have a strong correlation with ratings, but extremely short or long films did tend to receive more polarized scores.

Based on these patterns, we created a simple recommendation approach that highlights the highest rated movies within a selected genre, using minimum rating count thresholds to avoid recommending films with very little data. Although this is not a personalized system, it demonstrates how integrated datasets can support meaningful recommendation logic.

The final submission includes all required artifacts, including cleaned datasets, integrated files, plotted figures, tables, automated workflow scripts, metadata documentation, a data dictionary, and instructions needed to reproduce our entire process. All work complies with the terms of use and licensing restrictions of the original data sources. The report aims to be transparent and easy to follow so that someone else can repeat or extend our work.

-------------------------------------------------------------------------------------------------------------------------------------

 Data Profile

Our project relies on two primary datasets that are widely used in research on recommender systems and film analytics: the MovieLens 100k dataset from GroupLens Research and the Movies Metadata collection originally compiled from The Movie Database (TMDB) and distributed via Kaggle. These two datasets complement one another—MovieLens provides reliable user rating behavior, while the TMDB dataset includes rich descriptive metadata about movies. Integrating them allows us to analyze how movie characteristics relate to user ratings and to construct simple recommendation tools. Although both datasets are publicly available, each comes with its own ethical and legal considerations, which we carefully reviewed and incorporated into our workflow.

The MovieLens 100k dataset serves as the behavioral backbone of our project. It contains approximately 100,000 ratings made by about 600 users on nearly 9,000 movies. The key files we used are ratings.csv, which records userId, movieId, rating (on a 0.5–5 scale), and a UNIX timestamp, and movies.csv, which includes each movieId along with a title and a pipe-delimited string of genres. One of the most important aspects of MovieLens is its strong commitment to ethical data handling. The dataset is fully anonymized, meaning that userIds cannot be traced back to real individuals. No demographic information—such as age, gender, or location—is included or used in our project. This significantly reduces any privacy concerns, as the dataset contains no personally identifiable information (PII) or sensitive human subjects data. Legally, the dataset is licensed under Creative Commons Attribution 4.0 (CC BY 4.0), which allows redistribution and adaptation as long as proper credit is given to GroupLens Research. This license enables us to include the MovieLens data directly within our GitHub repository and use it throughout our analysis without restriction.

The second major component of our project is the Movies Metadata dataset, distributed on Kaggle and originally collected from the TMDB API. This dataset includes a wide range of descriptive attributes such as film titles, budget, revenue, runtime, release dates, popularity, and genre information in JSON-like structures. Files such as movies_metadata.csv and credits.csv provide detailed information that allows us to enrich MovieLens ratings with additional context. Unlike the MovieLens dataset, the TMDB-derived metadata does not fall under a standard Creative Commons license. Instead, it is governed by the TMDB API Terms of Use, which explicitly permit academic and non-commercial analysis but restrict redistribution of the full dataset onto public platforms such as GitHub. Because of these restrictions, we do not store the full TMDB metadata directly in our repository. Instead, we host these large files in a private Box folder accessible only to the course teaching staff. This complies with the licensing terms while still allowing reproducibility of our workflow, since users can download the data directly from Box and place it into the project’s IS 477 Project/ folder following the instructions in our README.

While both datasets are publicly available, they required substantial preprocessing due to structural differences and limitations inherent to each source. The MovieLens dataset is small and cleanly formatted, but the genre information is stored in a pipe-delimited string that needed to be converted into a list structure for ease of analysis. The timestamps also required conversion from UNIX format into human-readable dates. The TMDB metadata, on the other hand, contained numerous issues related to data quality. The id column, which we needed for merging with MovieLens, contained both numeric and non-numeric entries, missing values, and errors that had to be cleaned or filtered out before integration. Other fields such as budget, revenue, and runtime included zero or unrealistic placeholder values that required additional scrutiny. Release dates were inconsistent, with some films missing dates entirely or containing invalid formats. The genres column contained nested JSON-like strings that needed to be parsed into structured lists. All of these issues were addressed during the data cleaning stage, and detailed documentation of these decisions is included in our Week 3 notebook.

A key limitation in the integration process is that MovieLens movieIds do not perfectly align with TMDB metadata IDs. Although a large portion of movies match correctly, many MovieLens films do not exist in the TMDB metadata, and some TMDB entries do not appear in MovieLens. As a result, our merged dataset contains a subset of movies that exist in both sources. We recognized this limitation and discuss its implications in our findings, noting that some genres or years may appear underrepresented simply because they were not matched during integration.

Ethically, both datasets pose minimal risk because they involve cultural artifacts (movies) and public metadata rather than human subjects information. However, we still practiced careful data stewardship by ensuring that all files subject to licensing restrictions were handled appropriately and not redistributed in ways prohibited by their owners. We also provided full citations, licensing information, and a clear description of how to obtain the restricted data from Box.

Together, these datasets provide a robust foundation for exploring relationships between movie characteristics and viewer ratings. MovieLens offers highly reliable and well-formatted behavioral data, while the TMDB metadata adds depth, allowing us to examine how attributes like genre, runtime, and release year correlate with audience preferences. By merging them, we create a richer dataset that supports both exploratory analysis and simple film recommendation techniques. The attention to licensing, storage, and ethical considerations ensures the project remains compliant, transparent, and reproducible.
-------------------------------------------------------------------------------------------------------------------------------------

Data Quality Summary 

A major portion of our project involved assessing and improving the quality of both the MovieLens ratings dataset and the TMDB metadata dataset, as each presented different types of issues that had to be resolved before meaningful analysis or merging could occur. Although both datasets are widely used in educational and research contexts, neither is “ready to merge” straight out of the box. The MovieLens dataset is relatively clean and standardized, but still contains formatting inconsistencies and missing contextual information. The TMDB metadata, in contrast, is considerably larger and more complex, and required substantial cleaning across multiple fields. Our data quality process focused on identifying missing values, inconsistent formats, mismatched IDs, incorrect datatypes, and unrealistic or placeholder values, as well as ensuring that key fields were complete and reliable enough to support integration.

We began by profiling the MovieLens ratings dataset. The ratings.csv file itself is fairly well-structured, with four columns—userId, movieId, rating, and timestamp. However, the timestamp column is stored as a UNIX integer, which is not directly interpretable. To improve readability and support potential time-based analysis, we converted these values into human-readable datetime formats. We also checked for invalid or missing ratings, but the MovieLens dataset is known for its consistency, so no major corrections were needed. The rating scale (0.5 to 5.0 in 0.5 increments) was confirmed to be clean and free of outliers outside the permitted range. For movies.csv, we encountered more substantial issues. The genres column is stored as a pipe-delimited string (e.g., "Comedy|Romance"), which is inconvenient for analysis. We converted these strings into proper Python lists, ensuring each genre could be individually accessed and analyzed. Another issue was the title column, which sometimes included the release year in parentheses. While this is helpful visually, it is not ideal for programmatic analysis. We extracted the release year using a regular expression and added a new release_year column, allowing us to analyze rating trends over time. Some titles lacked a valid year, and those cases were filtered out, as they could not contribute meaningful historical information.

The TMDB metadata presented considerably more challenges. The dataset includes a large number of fields, some of which are inconsistently formatted, incomplete, or irrelevant to our project. The id column, which needed to match the MovieLens movieId, contained a mix of numeric IDs, non-numeric values, missing cells, and malformed entries (e.g., strings like "1997-08-20" showing up in the ID field). We converted the column to numeric where possible and filtered out rows with invalid IDs. This cleaning step was critical because mismatched or unusable IDs would disrupt the merging process and introduce bias into the integrated dataset. Datatype inconsistencies were common across other fields as well. The budget and revenue fields, for example, contained a large number of zeros or impossibly low values that were clearly placeholders rather than actual financial information. Since these fields were not central to our project’s analysis, we retained them but noted that they were unreliable and should not be used for interpretive analysis without additional cleaning.

The runtime column suffered from a similar issue. While many films had accurate runtimes, others recorded values of zero, extremely short durations, or blank entries. We identified these cases and treated them cautiously in our analysis. Some runtime values were retained as-is, but runtime was considered an exploratory feature rather than a core variable driving the recommendations. The release_date column also had inconsistencies—some dates were missing entirely, while others contained invalid formats or placeholder values. We standardized this column by converting valid entries to datetime objects while dropping rows with unparseable dates. This allowed us to compute release years reliably, although some metadata rows had to be excluded.

The genres column in the TMDB dataset is structured as a JSON-like string that often includes nested objects. This required parsing via ast.literal_eval or manual cleaning to extract the genre names into a usable Python list. Even after parsing, genre lists sometimes contained inconsistencies, such as duplicate genre names or missing genre arrays. We cleaned these cases by ensuring each movie received a standardized list of genres. Although this processing was more involved than the MovieLens genre cleaning, it ultimately allowed us to better interpret genre–rating relationships during exploratory analysis.

One of the most significant quality concerns was the mismatch between MovieLens movieIds and TMDB metadata IDs. Because the two datasets were not designed to work together, many MovieLens entries did not have a corresponding TMDB record and vice versa. After cleaning both ID fields, we merged the datasets and noted that several thousand MovieLens movies did not appear in the TMDB metadata. These unmatched rows were necessarily excluded from the integrated dataset. While this reduces the total number of observations available for analysis, it is a known and unavoidable limitation of cross-dataset integration. It also helps explain why certain genres or years appear more strongly represented in the final dataset: only films present in both sources survive the merge.

To address these issues systematically, we documented every cleaning step in our Week 3 and Week 4 notebooks. We also saved intermediate cleaned datasets such as ratings_clean.csv and movies_clean.csv, and produced a final merged dataset (merged_pipeline_output.csv) that passed all our quality checks. By the time we reached our exploratory analysis and recommendation stages, the data was complete, consistently formatted, and reliable for answering our research questions. Overall, the data quality assessment reinforced the importance of careful cleaning and validation, especially when integrating datasets that have never been linked before. Our detailed approach ensured that our analysis was accurate, reproducible, and grounded in well-prepared data.

-------------------------------------------------------------------------------------------------------------------------------------

Findings

Our analysis produced several meaningful findings about how MovieLens users rate films and how those ratings relate to attributes such as genre, release year, runtime, and overall popularity. By integrating the MovieLens ratings with TMDB metadata and performing exploratory visualizations, we were able to identify clear patterns that help explain why certain types of movies receive higher ratings while others exhibit greater variability.

One of the strongest patterns we observed involved average ratings across genres. After cleaning and transforming the genre data into list format and “exploding” the dataset so each movie–genre pair could be analyzed individually, we computed the mean rating for every genre. Genres such as Drama, War, Crime, and Mystery consistently ranked among the highest, each with average ratings well above the overall dataset mean. These genres tend to feature more serious storytelling, character-driven plots, and films traditionally favored by critics, which may explain their strong performance. In contrast, genres like Horror, Fantasy, and Children showed lower averages and noticeably wider spreads. For instance, the Horror genre contained many movies rated between 2.0 and 3.0, with only a small handful scoring extremely high. This pattern suggests that these genres are more polarizing—some films become cult favorites, while many others receive lukewarm audience responses.

We also evaluated rating trends by release year by extracting release years from movie titles and grouping ratings accordingly. Ratings peaked prominently in the mid-1990s through early 2000s, particularly among films released between 1994 and 1999. This period includes many widely acclaimed movies such as The Shawshank Redemption, Se7en, The Usual Suspects, and Pulp Fiction, all of which appear frequently at the top of public “best films” lists. Meanwhile, films released before the 1970s showed substantial variability, which may be tied to both stylistic differences in early cinema and the fact that older movies often accumulate fewer ratings in the MovieLens dataset than modern films. This imbalance impacts aggregate ratings and highlights the importance of evaluating rating counts alongside averages.

We also visualized the overall distribution of ratings across the dataset. The resulting histogram revealed a strong concentration between 3.0 and 4.0, with very few ratings at the extremes of 0.5 or 5.0. This aligns with earlier research on MovieLens: users generally avoid extreme ratings and instead express moderate approval. The shape of the distribution suggests that average ratings near 3.5 are not exceptional but instead represent the typical pattern of user behavior on the platform.

We explored whether runtime showed any meaningful correlation with ratings. Although longer films tended to show slightly higher average ratings, the relationship was inconsistent and weak, suggesting that runtime alone is not a strong predictor of audience reception. Movies with runtimes under 90 minutes, for example, were not systematically rated lower than those exceeding two hours.

Finally, after completing our exploratory analysis, we used the cleaned and merged dataset to build simple recommendation functions. Our genre-based recommender identified top films within categories such as Drama, filtering for movies with a minimum number of ratings to avoid unreliable outliers. For example, the highest-rated dramas displayed average scores above 4.2, demonstrating the genre’s strong overall performance. Our year-based recommender similarly identified the highest-rated films for a given release year, such as 1995, where films like Toy Story and Se7en emerged as top choices. These recommenders confirmed the patterns observed in our exploratory visualizations and provided practical examples of how integrated metadata can support meaningful recommendations.

Overall, the findings show that combining behavioral rating data with descriptive metadata reveals clear trends in audience preferences. Our integrated analysis demonstrates that genre and release year are strong determinants of ratings, whereas runtime plays a minor role. The results highlight how even a straightforward integration pipeline can produce interpretable insights and functional recommendation outputs.

-------------------------------------------------------------------------------------------------------------------------------------
Future Work 

While our project successfully integrated the MovieLens ratings data with TMDB metadata and produced meaningful insights and simple recommendation tools, there are several directions in which this work could be expanded or strengthened. Completing this project also taught us important lessons about data cleaning, dataset integration, reproducibility, and the challenges of working with large heterogeneous data sources. This section reflects on those lessons and outlines realistic avenues for future improvements.

One of the biggest lessons we learned was how much time and effort goes into data cleaning and quality assessment before any analysis can begin. Even datasets that are widely used and publicly available—like MovieLens and TMDB—are far from perfect. MovieLens has a clean structure, but the genre encoding, timestamps, and titles required significant preprocessing to be useful in analysis. The TMDB metadata, in particular, contained numerous inconsistencies such as non-numeric IDs, malformed dates, missing runtimes, and JSON-like fields that needed parsing. A large portion of our project timeline was spent identifying these patterns of inconsistency and designing cleaning steps to standardize them across thousands of rows. Moving forward, more automated quality checks or a validation script could improve this process. For example, we could develop a dedicated Python module that validates datatypes, flags invalid values, automatically cleans malformed IDs, and produces a data quality report summarizing all identified issues. Having such tools in place at the beginning of the project would make future iterations more efficient and reproducible.

Another major takeaway was the challenge of cross-dataset integration when the datasets were never originally designed to work together. MovieLens and TMDB use different identifiers, contain different subsets of films, and occasionally record film information differently. As a result, a large number of movies could not be matched across datasets, which reduced the size of the final merged dataset. In a future version of this project, we could explore more sophisticated matching strategies beyond direct numeric ID matching. For example, fuzzy matching film titles using algorithms like Levenshtein distance or incorporating release years as secondary keys could help increase the percentage of matched films. Additionally, using external bridging datasets—such as the “links.csv” file provided in other MovieLens datasets—could improve the mapping between MovieLens movieIds and TMDB IDs. Strengthening the integration process would allow for richer and more comprehensive analysis.

Another area for future expansion is the depth of analysis. Our project focused primarily on how ratings vary by genre and release year, along with simple runtime analysis. These attributes represent only a small subset of what the TMDB metadata contains. Future analyses could incorporate a wider range of features, such as cast information, crew details (e.g., directors and writers), budget-to-revenue ratios, or film popularity metrics. Including features like director or actor profiles could reveal patterns such as whether certain directors consistently produce highly rated films or whether star power correlates with stronger audience ratings. Incorporating revenue and budget data could also allow us to explore whether financial investment influences perceived movie quality. These deeper analyses would require more robust cleaning of metadata fields and possibly additional external datasets, but they would significantly enrich the insights we could produce.

We also see substantial potential for enhancing the recommendation system. Our current recommendation functions are intentionally simple, relying on average ratings and minimum rating thresholds. While this approach is easy to interpret, it does not reflect the more sophisticated recommendation algorithms used in real-world systems. Future work could involve implementing collaborative filtering techniques such as matrix factorization, user–item similarity models, or even neural network–based recommenders. These methods could produce personalized recommendations that account for individual user preferences and viewing histories rather than global rating averages. Additionally, content-based recommendation methods could use metadata features—such as genres, keywords, cast members, and plot summaries—to recommend movies similar to those a user already enjoys. Building these models would require rethinking our data pipeline to incorporate user-specific features, but it would greatly enhance the practical utility of the project.

Another major area for improvement involves workflow automation and reproducibility. While our project is reproducible through the sequence of notebooks and documented cleaning steps, it currently requires manual execution. Future work could involve implementing a full workflow automation system using tools like Snakemake or Makefile. This would allow the entire pipeline—from data download, to cleaning, merging, analysis, and output generation—to run through a single command. Not only would this strengthen reproducibility, but it would also make it easier to update the project if new data becomes available. Additionally, we could improve reproducibility by containerizing the environment with Docker so that anyone running the project would have exactly the same software dependencies and library versions.

Overall, this project gave us hands-on experience with data integration, cleaning, visualization, and reproducibility. Looking forward, there are many opportunities to expand the analysis, improve the technical infrastructure, deepen the recommendation system, and make the workflow more scalable and automated. These enhancements would transform our foundational exploration into a more powerful and professional-grade data science project.

-------------------------------------------------------------------------------------------------------------------------------------
Reproducability 

To reproduce all results, follow the steps below.

Clone the repository by running
git clone https://github.com/jsheryl909/Xing-Sheryl.git

and then navigate into the project folder.

Install all required Python packages using
pip install -r requirements.txt.

Download the large TMDB metadata files from the Box link provided in the report.
These include movies_metadata.csv, credits.csv, and any other metadata files.
Save all of these files inside the folder named "IS 477 Project" in the repository.

Make sure your folder structure matches the expected layout.
Inside the “IS 477 Project” folder, you should have ratings.csv, movies.csv, movies_metadata.csv, credits.csv, and any other files downloaded from Box.

Open the Jupyter notebooks and run them in the following order:

data_cleaning_week3.ipynb

data_integration_week4.ipynb

exploratory_analysis_week5.ipynb

recommendation_and_pipeline_week6_7.ipynb

Run each notebook from top to bottom without skipping any cells.

After running the notebooks, check the outputs folder.
It should contain tables such as merged_pipeline_output.csv, top_drama_recommendations.csv, and top_1995_recommendations.csv, as well as all generated figures inside the figures subfolder.

Compare your generated results with the ones shown in the final report.
The visualizations, tables, and recommended movies should match the results described in the Findings section.

-------------------------------------------------------------------------------------------------------------------------------------
References

MovieLens Dataset (GroupLens)
Harper, F. M., & Konstan, J. A. (2015). The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems.
https://grouplens.org/datasets/movielens/

Movies Metadata (TMDB via Kaggle)
Banik, R. (2017). The Movies Dataset. Kaggle.
https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset

-------------------------------------------------------------------------------------------------------------------------------------
Python Libraries

pandas

numpy

matplotlib

seaborn

scikit-learn

-------------------------------------------------------------------------------------------------------------------------------------