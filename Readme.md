## venmo money, venmo problems

## Design:
**Motivation:** What is venmo used for? Apply NLP techniques to analyze venmo transactions.

Some specific motivating questions:
Do the type of transactions change over time? For example, during football season, there could be betting/fantasy football pools that have transacations for football. Post-covid, Has there been a change in the social outings, rent/utilities payments? Can I detect tips and professional jobs on Venmo? Can I identify superusers? What transactions are the superusers doing?  
***while this project does not get around to answer all these questions, those that aren't remain potential for Future Work***

## Presentation:
[Slide Deck](00_venmo.pdf)

## Approach:



### Data
[01_Data_Collection](01_Data_Collection.ipynb)  
- Using venmo-api, data was collected from venmo on 8/9.
- API capabilities:
    - Search for users based on name
    - Pull transactions for each user (limit of 50 latest transactions, though there may be another way around this)
- Because the API does not allow pulling from a feed of the most recent transactions, to get a list of transactions, the following process was adopted:
    1. Find the most popular American names, based on information from the Social Security Administration
    2. Using searches for those names, generate a list of users (with more users for the more popular names)
    3. Pull transactions for each of the users
    - Note that this process results in data that is intended to reflect the broad population of U.S. Citizens and their usage of Venmo.

*Note: For privacy considerations, individual transaction data is not be available in the public repo. This includes raw data, processed data, and outputs within notebooks.*

[02_Data_Processing](02_Data_Processing.ipynb)\
- NLP to clean the data
- Handles Emojis
- Custom processing to allow for word embeddings from Google's file to be used (e.g. french_fries instead of "french fries")

[03_EDA](03_EDA.ipynb)
- Initial EDA performed on the data


### Modeling  
#### Initial Modeling
- Explored dimensionality reduction techniques (LSA, NMF, LDA). However, these were not that interpretable.
[04A_Modeling_spaced_notes](04A_Modeling_spaced_notes.ipynb) - adding spaces\
[04B_Modeling_defined](04B_Modeling_defined.ipynb)\
[04C_Modeling_single_defined](04C_Modeling_single_defined.ipynb)\
[04D_Modeling_demoji_notes](04D_Modeling_demoji_notes.ipynb)\
[04E_Modeling_single_demoji_notes](04E_Modeling_single_demoji_notes.ipynb)

#### Ultimate Modeling
- This was the final approach to developing themes for each note
- [05_Word_Embeddings_download](05_Word_Embeddings_download.ipynb)
    - obtain word embeddings for the word2vec google-news-200 dataset
- [06_Word_Vector_Matrix](06_Word_Vector_Matrix.ipynb)\
    - Convert each transaction note into word count vectorizer
    - Apply word embeddings
    - Result in vector for each note
- [07_Modeling_Clustering](07_Modeling_Clustering.ipynb) #This is the Champion Model
    - Use Kmeans cluster to arrive at themes for each note
    - Export dataset with themes

### Exploratory Data Analysis
- Performed additional data analysis using the final dataset in tableau
- [08_venmo_tableau_workbook](08_venmo.twb)

## Tools:
- Word Embeddings:
    - Google-news-300
- Python libraries
    - venmo-api
    - emoji
    - pandas
    - sklearn
    - seaborn
    - matplotlib
    - gensim
    - pyLDA
    - re
- Tableau
    - visualization

## Data source:
Venmo
Social Security Administration (for common names)

## Future Work:
- File cleanup:
    - Can add more discussion to the 04 models, to better illustrate why those were not used
