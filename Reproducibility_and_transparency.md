For our project, we organized all code, data, and outputs so that someone else can fully reproduce our analysis from start to finish. All project code and notebooks are stored in our GitHub repository, and all key output data files are uploaded to a shared Box folder. Together, these form a reproducible package that captures both the workflow and its results.

Steps to Reproduce Our Results

To reproduce our analysis, a user should first clone our GitHub repository and download the data from our shared Box folder. The Box folder contains the merged and cleaned datasets as well as selected output files. After downloading, these files should be placed into the IS 477 Project directory inside the cloned repository, preserving the same file names and structure we used during development. Once the data are in place, the user can open our Jupyter notebooks (especially recommendation_and_pipeline_week6_7.ipynb and the Week 7 pipeline notebook) and run all cells in order to regenerate the cleaning steps, data integration, recommendation models, and visualizations.

Data Access and Box Folder

Because some of our output data files are not retrieved programmatically and may be too large or inconvenient to store directly in GitHub, we host them in a Box folder that is shared with the course staff:

Box folder link: https://uofi.box.com/s/0v4vb6sdzid4cdbtkn4ch00qsx5rsumw

This folder includes files such as merged_pipeline_output.csv, genre- and year-based recommendation outputs (e.g., top_drama_recommendations.csv), and any other derived datasets used in our final analysis. In our report, we clearly state that these files should be downloaded and placed into IS 477 Project/ within the project directory so that all notebook paths resolve correctly. We also ensured that the Box folder permissions allow access to the TAs; if there is any doubt, we plan to confirm this via Campuswire before the deadline.

To avoid committing large or external data to GitHub, we add the local path where Box data are stored to our .gitignore file. This prevents accidental pushes of large files while still allowing the TAs to retrieve them using the Box link.

Code, Workflows, and Output Artifacts

All code needed to reproduce our results is contained in the Jupyter notebooks stored in the repository. These include:

The Week 3 cleaning notebook, which documents data quality checks and cleaning operations.

The Week 4 integration notebook, which merges MovieLens ratings with metadata and resolves key mismatches.

The Week 6–7 notebook (recommendation_and_pipeline_week6_7.ipynb), which implements and explains our recommendation logic and visualizations.

The Week 7 pipeline notebook, which defines functions to load, clean, and merge the data and provides a run_full_pipeline() entry point for end-to-end execution.

Our results include both intermediate and final output files (e.g., cleaned and merged CSVs, recommendation tables) as well as visualizations embedded directly in the notebooks. By combining code, data, and outputs in one structured package, we make it straightforward for someone else to trace how each figure or table was produced.

Software Dependencies and Environment

To document our computational environment, we provide a requirements.txt file listing the core Python packages and versions used in our analysis (for example, pandas, numpy, matplotlib, seaborn, and scikit-learn). We also capture the full set of installed packages using the output of pip freeze, which can be used to recreate our environment more precisely if needed. In our documentation, we note that the project was run using Python 3.x on a Windows machine, but the code should be portable to other operating systems as long as the same dependencies are installed.

Licensing

We explicitly document the licenses associated with the datasets and software used in our project. The MovieLens dataset is licensed under CC BY 4.0, and the TMDB-based metadata follows the TMDB API Terms of Use; we include links and attribution in our report. Our own code and documentation are released under an open-source license (e.g., MIT or a similar permissive license), which is included as a LICENSE file in the repository. This clarifies how others may reuse our code and results while respecting the licensing terms of the original data providers.