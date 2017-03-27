# Document distance as transport in word space

by Matt J.Kusner (Alan Turing Institute)

Goal: similarity between documents

Eg.
- recommendation
- ranking (web search)
- similarity of recipe


How to compute similarity?

### Attempt 1
- bag of words ( number of times words occur in each document)
- very sparse
- similarity
  - euclidean distance
- short coming
  - two unrelated documents can have similar words and thus doesn't work well
  
### Attempt 2
 - use word embedding
   - euclidean distance in embedding space
   - everything else same as Attempt 1
   
How can we leverage these high quality word embedding?

- Normalise the TF
- constructs a doc representation
  - weight with prob masses and then 
  
- word mover's distance
 -  min word cost to transport d to d'.
   - optimization problem
   - like earth mover's distance (optimal transport)
   
## Does it work?

 - test document Harry document
    - compared with marginalised stacked denoising (mSDA)
      - essentially noisy auto encoder
      - train each layer individually
    - also with TF-IDF, BoW, LDA, LSI using KNN
    
 - Sentence Classification
    - compared with skip thought vectors
      - rnn to predict surrounding sentence from middle sentence

## Computation Complexity
  - optimization problem is O(n^3log n), number of unique words in doc.
  
#### Approximation 1 (Word Centroid distance)
  - inflate each words embedding by TF.
   - then normalize using centroid
   - then compute euclidean distance
  
#### Approximation 2 ( remove the last contraint) 
  - then just find the nearest neighbour
  
   

    
   
 



