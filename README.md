# NAR-Data-Discovery
Nucleic Acids Research Data Discovery

## Purpose
This is an exploratory project interested in using an archive of papers from a major biology research database (NAR)
as well as the Natural Language Processing model of `Doc2Vec` to identify trends, topics, and similarities in publications
over time. We are hopeful that this analysis could generate interesting conclusions about the direction the field of 
Biology is headed, and that several novel visualizations may be produced.

## Notebooks
Below you will find a list of notebooks that serve as the building blocks of this project. 
We are always looking for feedback or suggestions on how to improve any of the steps in the pipeline, 
and anybody is welcome to reproduce and modify all of this work if it could help you in any way.

### Part 1: Web Scraping and Downloading Files
- Crawls URLs from `nardb.txt` of article year pages contained in the [NAR Issue Archive](https://academic.oup.com/nar/issue)
- Produces list of all article links to download
- Downloads all of relevant article html files and stores them in `articles` directory
### Part 2: Article Data Extraction and Removal of Irrelevant Pages
- Processes title, abstract, introduction, and author name into `original-article-data.csv`
- Remove articles lacking useful information (editorial editions, advertisements, or lacking needed parameters)
- Places all data into `complete-article-data.csv` for later processing
### Part 3: Data Pre-Processing
- Perform input sanitization, lemmatization, removal of stopwords
- Use TF-IDF weighting to determine words to remove from corpus
- Output results from documents into `preprocessed_data.csv`
### Part 4: Train our Model
- Train a `Doc2Vec` instance and save the model's resultant embeddings in `doc_embeddings.npy`
- Perform self-similarity "sanity checks" to ensure embedding is useful
### Part 5: Clustering Techniques
- Using various clustering techniques, establish clusters of different documents 
- All prior data, cluster numbers, along with PCA components are all stored in `cluster_results.csv`
### Part 6: Visualizing our Data
- Use cluster assignments and PCA components of document embeddings to visualize cluster groupings

## Current Data (feel free to use)
The aggregate data we've accrued over time can be found within the file `cluster_results.csv` consisiting of: 
- `year`: year of article publication
- `article-link`: original link to the article
- `local-path`: local path in the `articles` folder where one can find page source
- `title`: the paper or article's title
- `abstract`: the paper's abstract (editorial articles, by their nature, lack an abstract)
- `authors`: a list of all contributing authors to the papers
- `introduction`: all text contained within the introduction of the article (or
  a similar area, we occasionally didn't have labels for the introductions)
- `preprocessed_data`: all text after Part 3's preprocessing with words separated by spaces
- `pca_feature*`: Principle Component Analysis values (note total explained variance is only around ~10% 
even when accounting for all 3 features). These features are used to represent individual articles in 2D 
and 3D space in Part 6.
- `xmeans_cluster`: cluster assignment based on the XMeans algorithm
- `kmeans_cluster`: cluster assignment based on the KMeans algorithm
