# A Comparative Analysis of IR Models for Book Search Systems
*Final project repo for INFO 556 - Spring 2026*

**Author: Colleen Feaman**


## Objective
The purpose of this project is to answer the question, “Which search model performs best for relevant book discovery?”. This repository simulates a real-world search system and evaluates three information retrieval (IR) models on a large book dataset. The project enables comparison between these models and provides insight into which approach is most effective for retrieving relevant results in a book search context.

The IR models:
- Boolean Retrieval Model: returns documents that exactly match the query
- Vector Space Model: returns documents based on relevance using TF-IDF weighting and cosine similarity
- BM25 Probabilistic Model: returns a ranked list of documents based on term frequency, document length, and inverse document frequency

The metrics for comparison:
- Precision: measures the proportion of retrieved documents that are relevant
- Recall: measures the proportion of all relevant documents that are retrieved
- nDCG: measures the quality of the ranking by giving higher importance to relevant documents that appear earlier in the results list

## Data
The data used for this project can be found here: https://www.kaggle.com/datasets/saurabhbagchi/books-dataset

There are three files in the dataset; however, `books.csv` is the only file used for this project.


## Usage Instructions

Key considerations:
- The code for this project is tailored to the data file already in the repository
- Cells where user input is intended are clearly captioned with `#USER INPUT`

Ensure the repository looks like this:
```text
INFO-556-PROJECT-IR-SYSTEMS/
├── data
    └── books.csv
├── project.ipynb
├── README.md
└── user-input.ipynb
```

**The following instructions are intended for the use of the `user-input.ipynb` file:**

1. Scroll down to the section titled *"Evaluation Set Up"*
    - See the first cell in that section captioned *"#Set evaluation queries"*
        - This cell is where you will add your set query terms for model evaluation
    - First, run all cells above that cell (this will load the libraries and data, and perform the EDA and preprocessing)
    - Next, replace the red text in the cell using your own query terms, then run it
        - *Note:* There are placeholders for three terms, but you can use as many or as few terms as you would like. For example:
        ```python
        queries = [
        "world war history",
        "stephen king",
        "harry potter",
        "financial management"
        ]
        ```
2. Run the following three cells
    - As captioned, in order:
        - *"#Standardize outputs"*
        - *"#Combine all model results into one pool"*
        - *"#Add relevance labels"*
3. See the cell captioned *"#Manually add relevance to each book"*
    - This cell prompts you to label book results from the query with a relevance label. Before running the cell, decide how many books you would like to label. It is already set at 40.
        - If you only want to label 10 books, then replace the 40 with 10. For example:
        ```python
         for i in range(10):
        ```
    - Now run the cell. The system will display the query, a book title, and the author. It will prompt you to enter a relevance label. There are only two options:
        - 1 = relevant
        - 2 = not relevant
        - *Note:* To decide relevance, consider if the book displayed matches any of your set query terms. For example, if one of your set query terms is "world war history" but the book is about a civil war, that is not relevant, and you would enter a 2
    - After inputting a 1 or 2, hit enter, and the next book will populate
        - *Note:* There is no time limit here, you can do an external search of the book to ensure you input an accurate label
    - Once your selected amount of books are labeled, the cell will finish running
4. Run the next cell captioned *"#Check unlabeled books"*
    - This cell displays a table of remaining books lacking a relevance label
    - If no results populate, move on to Step 5
    - If results do populate, look at the following cell captioned *"#Fix unlabeled books"*
        - There are two lines of code prepared to add relevant vs. not relevant labels. Add the index number of the book to the correct lines. For example:
        ```python
        pool_df.loc[[4, 6, 10], "relevant"] = 1
        pool_df.loc[[1, 3, 5], "relevant"] = 2
        ```
        - If you only need to run one of the lines, simply add a `#` at the front of the line of code. For example:
        ```python
        #pool_df.loc[[<enter relevant index numbers here>], "relevant"] = 1
        pool_df.loc[[7, 8], "relevant"] = 2
        ```
        - Once ready, run the cell
5. Run the next cell, captioned *"#Ensure all results have a relevance label"*
    - This cell displays a table of how many documents were populated for each query for each model by grouping the documents by their relevance label
    - This cell also ensures that all results have a relevance label. If you see a column for 0, you'll need to re-do Step 4
6. Lastly, you can run the remaining cells
    - The final two cells will display tables that are intended for you to evaluate the effectiveness of the models
        - The second to last cell captioned *"#Retrieval Performance by Model Per-Query"*
        - The last cell captioned *"#Average Retrieval Performance by Model"*
        - *Note:* Higher scores = better results

