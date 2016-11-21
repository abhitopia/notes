# [Smart Reply](https://arxiv.org/abs/1606.04870) ( from Google)
* novel end-to-end method for automatically generating short email responses
* system is currently used in Inbox by Gmail
* responsible for assisting with 10% of all mobile responses.

## Computation



## Algorithm
- **Preprocessing**

Data collected is message and reponse pairs. ( For triggering model, also messages with no response collected)
 - Language Detection
 - Tokenization 
 - Normalization (infrequent words removed. entities like names, URLs, addresses, replaces with special tokens)
 - Quaitation Removal
 - Salutation/close removal
 
- **Trigerring Model**
 - Features
  - after preprocessing extract content features
    - unigrams, bigrams, etc.
    - special signal like recipient in contact list, etc.
 - Architecture
   - Feedforward MLP
     - embedding layer.
       - vocabulary approx. 1 million words.
       - embedding separate for each sparse feature type( eg. unigram vs bigram)
       - aggregate features within one feature type and then concatenated to get dense input vector
     - 3 full connected hidden layers.
       - Relu
       - drop after each hidden layer
 - Optimization
   - Logistic loss cost function
   - Adagrad optimizer
   
- **Response selection**
 - 
- 

## Implementation


## Application

## Code




