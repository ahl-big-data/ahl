# Embedding
It will likely be best to construct this as an embedding system. In doing so, there will be a safe option and a more complex option.

### Safe Option: BERT
The simplest thing to do would be to use a pretrained sentence embedding model. We my still want to do some clever preprocessing. 

Arguably, the best of these models for developer experience is [SBERT](https://www.sbert.net/) with which I've already done some fiddling in our data exploration.

However, this may not be complex enough for our project. To form a comparative analysis, we could [retrain an OpenAI model](https://openai.com/blog/customizing-gpt-3), set up a query system, and compare the results.

### More Complex: Custom Text Embedding Model
Building a word text embedding model isn't incredibly difficult. TensorFlow has a pretty straightforward [example](https://www.tensorflow.org/text/guide/word_embeddings). Essentially, you pick a corpus and train an embedding model based on some token lists from real world sentences. We should do this over both paper and patent data.

Computing embeddings for sentences is potentially a bit more involved. You can find a great overview [here](https://aajanki.github.io/fi-sentence-embeddings-eval/models.html). For us, an easy entry point and predictive power might be to do pooling. Pooling works by using the values of word embeddings to produce a sentence embedding. You can make this quite simple by taking the average over word embeddings in a sentence.

A more involved method is known as contextual full sentence embeddings. This is essentially end-to-end training on sentences. Here there are two major increases in complexity, size of the input layer and generating the labels. The size of the input net is something we should comfortable enough managing at this point in the class. We can potentially generate labels using a thesaurus to generate slighly altered sentences and initial embedding values with an averaged word embedding model. 

### Recommendation
I recommend we go with two custom text embedding models using two models trained over both patents and papers. 
1. Pooling model using word2vec. 
2. Varied sentences with inital word2vec embeddings.

We can then compare the loss of these two models against SBERT. 

