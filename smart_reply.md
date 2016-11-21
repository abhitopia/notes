# [Smart Reply](https://arxiv.org/abs/1606.04870) ( from Google)
* novel end-to-end method for automatically generating short email responses
* system is currently used in Inbox by Gmail
* responsible for assisting with 10% of all mobile responses.

## Computation

- **Response Clustering**
  - cluser responses with same intent. 
    - Eg., _"Yes, I'll be there"_ has same intent as _"I will be there"_
  - diversity
    - ensure suggestions do not belong to same cluster.

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
       - **feature hashing** to bucket rare words not in vocabulary.
       - embedding separate for each sparse feature type( eg. unigram vs bigram)
       - aggregate features within one feature type and then concatenated to get dense input vector
     - 3 full connected hidden layers.
       - Relu
       - drop after each hidden layer
     - Logistic loss cost function
       - Adagrad optimizer
   
- **Response semantic intent clustering**

 Only frequent responses are taken for clustering purposes. Low quality responses such as those containing spelling errors, or  profanity, informal language, etc. are removed.
 - Canonicalize preprocessed responses
    - parse using **dependency parser**
    - use syntactic structure obtained to generate canonicalized representation
    - ignore
      - words (or phrases) that are modifiers
      - unattached to head words
 - Extract lexical features
    - ngrams of n upto 3
    - skipgrams of n upto 3
 - Graph construction
   - Response Nodes (V_r)
     - Labelled
       - thankyou_label, sorry_label, etc.
       - manually on top frequent responses
     - Unlabelled
   - Feature Nodes (V_f)
     - nodes containing lexical features extracted above.
   - create edges
     - (u,v) where u belongs to V_r, v belongs to V_f such that v belongs to feature for response u
 - Semi supervised learning
    - distributed [EXPANDER](https://arxiv.org/abs/1512.01752) framework for optimization
    - For equations, refer to original paper.
    - output is learned distribution of semantic intent label for every node.
    - Assign top scoring label as the semantic intent (filter out low scoring labels)
 - Discover new clusters
    - there may be clusters not labelled initially
    - Iterative propagation
      - first phase
        - labelled examples, 5 iterations.
      - second phase
        - fix cluster assignment after first phase
        - sample 100 nodes from yet unlabelled nodes
        - label new node as potential clusters
        - run again
      - subsequent phase
        - repeat second phase until convergence
        - convergence imply no new clusters are discovered, and members of the cluster don't change
  - Cluster Validation
     - extract top k members for each semantic cluster
     - provide (response, cluster label) and few example responses from same cluster
     - human raters to judge if response conveys same intent as cluster label and example responses
   
     
- **Response selection**
  - Sequence to sequence LSTM is used.
  - Training
    - input and output vocabulary consists of most frequent words
    - recurrent projection layer
      - substantially improved quality of converged model
      - substantially improved convergence time
    - gradient clipping
      - clipped at value 1
      - essential for stable training
    - SGD with Adagrad
  - Inference
    - Three ways to do inference
      1. Sample Response
         - sample output word at every time step and feed back as input in next time step.
         - repeat until <EOS> is output.
      2. Approximate most likely response
         - __Greedy Approach__
           - take most likely response at each time step, and feed back as input in next time step
         - __Beam Search__ (Less greedy approach)
           - take top _b_ tokens at every time step and feed them as input in next time step
           - then retain top _b_ best response prefixes and repeat
      3. Score existing candidate response (Used by Smart Reply)
         - feed in each token of the candidate response
         - use the softmax output to get the log likelihood of the next candidate token
         - sum loglikelihood of all the token in candidate response
    - Smart reply uses third approach  

## Implementation

## My thoughts
 - Confidence Model


