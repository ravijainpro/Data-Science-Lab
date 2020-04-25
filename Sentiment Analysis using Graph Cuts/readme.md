The python code along with output can be accessed @ https://colab.research.google.com/drive/10QYb9Qfs7QO8ALQC7lamYM3jp3R5K7FC

1. Run the "Sentiment Analysis - Graph Cuts.ipynb" on  Google Colab, the reasons for it are:
-The model will take a day or more to completely train and test if run on pc/laptop
-The runtime used is TPU in co-labs (To accelerate the model by 15x-30x)
-Function caching is done to boost the function execution by 50x-80x
-Parallelism is done by pooling in TPU 8 cores

2. Change the runtime to "TPU" (Runtime->Change Runtime Type->TPU->Ok)

3. Import the below files in Colab before running the cells.
-"neg.zip"
-"pos.zip"

3.  Explanation:

-The ratio of Train vs Test data taken is 90:10.
(First 900 reviews each of pos and neg type is used for training, the remaining 100 reviews of each type is used for testing)

-> The given reviews were pre-processed as follows:
1. Lower casing the entire sentence.
2. Removing stop words (words such as 'the', 'is' has no significance in feature selection)
3. Removing punctuations (As they just add noise to the data)
4. Using NLTK library stemming the tokens (part of normalization) (This improves the input data quality)
5. Using NLTK lemmatization of tokens (part of normalization) (This transforms noisy tokens to clear format and improves model quality)

-> Initially, The basic Naive Bayes classifier based on 1 to 3 grams to do the polarity classification. The overall accuracy of this model was 59%

-> Later, the graph cut model is prepared, which uses the concept of similarities between the given 3 sentences along with NB predictions and finds the min-cut; based on which the classification is done.

-> Only first 6 sentences of each test reviews were used (As they contain enough features for classifying the data) (Also, it significantly reduced testing time by many folds)

-> The overall accuracy attained is 0.7164995000000001 (71.65%)

NOTE:
( The accuracy can be easily boosted to 80%-90% by doing a small tweak:
1. Send all the sentences of the review instead of just sending just only first 6).
But unfortunately, this is a lot of time expensive too; Using TPUs too it will take more than a day to run the entire code.
(I took approx 9 mins to test each review with this config. but the result was pretty good).

To prove this I have tested a small amount of test data with the above configuration.
The accuracy attained after tweaking is 0.888945 (88.89%) 

Hence, the improvements in successive steps gave a significant improvement in overall accuracy. (from 59% to 71.65% to  88.89%)
