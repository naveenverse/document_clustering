# document_clustering

## Objective
To cluster research papers based on similarity of thier research.

## Approach 
Scape data from NCBI database to train a KMeans clustering model and visualising the topwords of clusters in wordcloud to understand the intuition trained model while clustering.

  ## Web scraping
  We scrape research articles from NCBI database using `Biopython` module.
  
    from Bio import Entrez
    
  We create a custom function to retrive the research articles using `Entrez`
  
 ## Preprocessing 
 We clean text, extract features and vectorize using `nltk`
 
    import re
    import string
    import random
     
    from nltk import word_tokenize
    from nltk.corpus import stopwords
    from nltk.stem import WordNetLemmatizer

    nltk.download('stopwords')
    nltk.download('wordnet')
    nltk.download('punkt')
  
  ## Model building
  We build a KMeans cluster model using `sklearn`
  
    range_n_clusters = list(range(2,11))
    clusters = []
    n_cluster = []
    inertia_vals = []

    for n_clusters in range_n_clusters:
      cluster_model = KMeans(n_clusters=n_clusters, random_state=5)
      cluster_model.fit(vectorized_docs)

      clusters.append(cluster_model)
      inertia_vals.append(cluster_model.inertia_)
      n_cluster.append(n_clusters)
    
   <img width="285" alt="elbow plot" src="https://user-images.githubusercontent.com/59974158/137441784-93403860-79f2-4d4e-a80e-57506763fd95.png">
The elblow curve plot suggested the model is best fit for `n_clusters=3`

## Visualization
The top words from each clusters are visualized using `wordcloud`

<img width="259" alt="elbow plot" src="https://user-images.githubusercontent.com/59974158/137442105-cafaf73a-7cc8-4930-bcbe-03f4585dc9ec.png">

      Top 10 words from cluster 0 :
      ['covid', 'cell', 'model', 'risk', 'sarscov', 'cancer', 'associated', 'factor', 'diabetes', 'expression']


  
 
