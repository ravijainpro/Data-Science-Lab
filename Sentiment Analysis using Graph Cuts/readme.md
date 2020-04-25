1. Run the "Sentiment Analysis - Graph Cuts.ipynb" on  Google Colab, the reasons for it are:
-The model will take a day or more to completely train and test if run on pc/laptop
-The runtime used is TPU in co-labs (To accelerate the model by 15x-30x)
-Function caching is done to boost the function execution by 50x-80x
-Parallelism is done by pooling in TPU 8 cores

2. Change the runtime to "TPU" (Runtime->Change Runtime Type->TPU->Ok)

3. Import the below files in Colab before running the cells.
-"neg.zip"
-"pos.zip"

3.  Explanation:

-The ratio of Train vs Test data taken is 80:20.
(First 800 reviews each of pos and neg type is used for training, the remaining 200 reviews of each type is used for testing)

-> The given reviews were pre-processed as follows:
1. Lower casing the entire sentence.
2. Removing stop words (words such as 'the', 'is' has no significance in feature selection)
3. Removing punctuations (As they just add noise to the data)
4. Using NLTK library stemming the tokens (part of normalization) (This improves the input data quality)
5. Using NLTK lemmatization of tokens (part of normalization) (This transforms noisy tokens to clear format and improves model quality)

-> Initially, The basic Naive Bayes classifier based on 1 to 3 grams to do the polarity classification. The overall accuracy of this model was 50% (Pretty low).

-> Later, the graph cut model is prepared, which uses the concept of similarities between the given 3 sentences along with NB predictions and finds the min-cut; based on which the classification is done.

-> Only first 6 sentences of each test reviews were used (As they contain enough features for classifying the data) (Also, it significantly reduced testing time by many folds)

-> The overall accuracy attained is 0.6834848484848486
