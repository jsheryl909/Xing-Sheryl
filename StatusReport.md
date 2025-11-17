CONTRIBUTIONS AND PDATE ON EACH TASK :

Week 1 & 2 - Collaboration both Sheryl and Xing

Xing and I collaborated during Weeks 1 and 2 to collect the datasets, review the terms of use, and set up a clean structure for our project. We have downloaded the MovieLens data and the accompanying movie metadata files, validated that both are publicly available and ethically appropriate for academic use, and then discussed how best to organize our workspace so that the project remains easy to navigate as it grows. After talking through a few options, we decided the simplest and most organized approach was to place all CSV files inside a dedicated IS 477 Project folder within our main XING-SHERYL directory. This setup keeps our data isolated in one place, prevents confusion about file paths, and ensures that both of us can easily reference the same folder structure when working on different parts of the project. We finished these foundational setup steps together so we could begin Week 3 without any hiccups to start the cleaning and analysis work.

Week 3 - Sheryl 

I performed the initial data cleaning work in Week 3 inside a Jupyter Notebook called data_cleaning_week3.ipynb, which resided in the XING-SHERYL/ project directory. I loaded all MovieLens and metadata CSV files from the IS 477 Project folder, first inspecting their shapes, data types, and overall structure. I standardized key columns such as userId, movieId, and rating to be stored as consistent numeric types, important for joining these datasets in the later steps. I then converted UNIX timestamps of MovieLens into dates, which are human-readable, and checked for missing values in each dataset. I removed any rows that were missing essential information, like movie IDs, titles, or ratings, in order to avoid problems during the analysis.

The majority of my cleaning work was invested in the movies dataset. Still working within data_cleaning_week3.ipynb, I extracted release years from the movie titles by identifying the four-digit year inside parentheses - for example, “Toy Story (1995)” → 1995. Then I filtered out movies with missing or unrealistic release years to keep future trend visualizations more accurate. I also cleaned the genre column by splitting the pipe-separated genre strings into Python lists, which will make genre-based analysis much easier moving forward. Going into the end of Week 3, I had created two cleaned and structured datasets, ratings_clean and movies_clean, which are now ready for integration and merging tasks in Week 4.

Week 4 - Xing 

During Week 4, my responsibility was to integrate the cleaned MovieLens ratings dataset with the cleaned movie metadata Sheryl produced in Week 3. I have completed all of this work in a new Jupyter notebook called data_integration_week4.ipynb, which is stored in the main project folder, XING-SHERYL/, so that both of us can access it easily. Rather than re-running the entire cleaning process of Week 3, I loaded in the cleaned output files that Sheryl produced—ratings_clean.csv and movies_clean.csv—both of which are stored inside the IS 477 Project/ directory.

The verification at the outset of the integration process was done in regard to the structure of each dataset: the number of rows, the unique movieId values, and confirmation that the data types of key columns matched across the two sources. Once this was confirmed, I performed the core task of Week 4: the merge of MovieLens ratings with the movie metadata on the movieId column using an inner join. This join tied every user rating to its corresponding movie title, release year, and genre information. After the merge, I assessed how successful the merge was, checking the count of distinct movie IDs before and after integration. Additionally, I identified movie IDs present in the ratings yet without a match in the metadata, along with movies in the metadata which had never been rated. Documenting such mismatches serves to explain why some records may not appear in the merged dataset. After completing the integrated dataset, I wrote the output into a new file named ratings_with_metadata.csv. It is housed inside the IS 477 Project/ folder. This now acts as the combined source across all exploratory analysis and visualizations for Week 5. As in Week 3, Week 4 has its own dedicated notebook, data_integration_week4.ipynb, so that every phase of the project is clearly separated. This structure-a single .ipynb file per week-keeps the workflow organized, making it easy for either of us to review, update, or troubleshoot any part of this process as the project continues.

Week 5 - Collaboration both Sheryl and Xing

During Week 5, the two of us proceeded to explore the data using the integrated dataset from Week 4. All that work is done in a new notebook called exploratory_analysis_week5.ipynb saved in the main XING-SHERYL project directory. We started by loading the merged dataset called ratings_with_metadata.csv from the IS 477 Project folder, which included user ratings along with each movie's title, genres, and release year. By starting with this combined data set, we were able to focus immediately on analysis without having to repeat any cleaning or merging steps.

The first part of our analysis covered the overall distribution of user ratings by visualizing a histogram of rating values. This provided us insight into how MovieLens users generally rated films. We then "exploded" movies with multiple genres and computed average ratings by genre to understand trends based on genre. That gave us an idea as to which types of movies generally get higher ratings. We examined changes over time, plotting average ratings by release year to see long-term trends across decades. Finally, when possible, we analyzed runtime compared to rating to see whether movie length impacts audience scoring.

All visualizations were created within the Week 5 notebook, and summary tables of means by genre and year were written out as CSVs for quick reference later in the project. By the end of Week 5, we had developed a solid comprehension of the patterns of ratings along a number of key dimensions, which would form the basis for higher-order insights in the coming weeks.

----------------------------------------------------------------------------------------------------

UPDATED TIMELINE : 

Although we completed the work for Weeks 1–5, we did fall slightly behind our original timeline and ended up finishing some pieces later than planned. Because of this, we have decided to combine the tasks for Weeks 6 and 7 so that the recommendation system and the automated workflow can be developed together. This adjustment will help us stay on track and ensure the full project is completed on time, with Week 8 still reserved for final documentation and polishing our results.

---------------------------------------------------------------------------------------------------

CHANGES TO PROJECT PLAN 

The overall structure of the project remains the same as described in our original plan; however, several improvements were made based on Milestone 2 feedback. First, we updated the plan to include direct URLs to both datasets, ensuring transparency and traceability. We also added the explicit licenses for the MovieLens dataset (CC BY 4.0) and the TMDB-based metadata (TMDB API Terms of Service). These details strengthen the ethical and reproducibility sections of the project plan.

A second change was the creation of a standardized file structure early in the project. After reviewing the plan in Week 2, my partner and I agreed that the cleanest and most reproducible approach would be to place all raw and cleaned data inside the IS 477 Project folder. This ensures that all notebook paths remain consistent and reduces the risk of broken links. Additionally, because the original credits.csv exceeded GitHub’s file size limit, we removed it from the repository history and adjusted our workflow so that only necessary datasets are version-controlled.

Finally, although we completed the tasks for Weeks 1–5, we fell a bit behind our original pacing and will be adjusting the plan slightly. Instead of handling Weeks 6 and 7 separately, we are now combining the recommendation system work and the automated workflow development into a single joint effort to ensure we stay on track for the final submission. Week 8 will still be dedicated to final documentation and polishing the report, and we expect to complete the project on time with this revised schedule.

Movie Lens Rating Dataset 

Direct Download:
https://files.grouplens.org/datasets/movielens/ml-latest-small.zip

Dataset homepage:
https://grouplens.org/datasets/movielens/

License:
Creative Commons Attribution 4.0 International (CC BY 4.0)
https://creativecommons.org/licenses/by/4.0/

Movie Metadata Set 

Dataset page:
https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset

Direct download link cannot be provided without a Kaggle token,
but this is the official dataset page

Source database:
The Movie Database (TMDB)
https://www.themoviedb.org/

License / Terms of Use:
TMDB API Terms of Service (covers metadata usage)
https://www.themoviedb.org/documentation/api/terms-of-use

--------------------------------------------------------------------------------------------------