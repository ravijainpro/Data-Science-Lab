1> Assignment 1:
First a sentence level classifer was modeled with ngrams as features. 
The accurracy attained by it was 82.88%

Then after labeling the sentence as "x" ('x' is an indian lang); 
we prepare binary classifers i.e., "x vs en" as the sentence is a mix of eng and a Indian lang
so, for this 8 binary classifieres were prepared using ngrams as features.
The train loss for each of the bianry classifier was close to 0.

Then above two layers were integrated and word level labeling was done..

Result: 

kn  accuracy:  0.8277591973244147
te  accuracy:  0.9325626204238922
bn  accuracy:  0.9773226042428675
hi  accuracy:  0.8745294855708908
mr  accuracy:  0.9757709251101322
ml  accuracy:  0.8040201005025126
ta  accuracy:  1.0
gu  accuracy:  0.15675675675675677


 Final overall accuracy is (by combining both the layers)  0.8946693533614215 



2> Assignment 2
For the same train and test dataset new model was prepared with features as described by the lecture video sent by Sir.

The words lvl data was a tuple => (word, sentence_lang, word_label)

The words of the givem sentence were put up in a list.. 
	i.e., [(word1,sentence_lang,word1_label),.....,(wordk,sentence_lang,wordk_label)]

So, for all given sentences such lists were formed and stored in another list()

Then features were made for the given dataset as mentioned by sir in the video.

using sklearn_crfsuit..with 0.1 as L1 AND L2 regularization, by setting all_possible_transitions and all_possibles_states to true and by using 'lbfgs' algo a model was prepared..

The result from the model was:

              precision    recall  f1-score   support

          mr      0.906     0.998     0.950       454
          hi      0.895     0.913     0.904      1593
          te      0.654     1.000     0.791       519
          ta      0.820     0.989     0.896       543
          kn      0.840     0.998     0.912       598
          gu      0.464     1.000     0.634       185
          bn      0.899     0.992     0.943      1368
          ml      0.753     0.980     0.852       199
          en      0.944     0.700     0.804      3850

    accuracy                          0.859      9309
   macro avg      0.797     0.952     0.854      9309
weighted avg      0.883     0.859     0.858      9309


To improve quality, Hyperparameter Optimization was done wuing scipy and sklearn library..
Regularization parameters were set by using randomized search and 3-fold cross-validation..
i.e., Fitting 3 folds for each of 50 candidates, totalling 150 fits.. (Time consuming but effective)

The result was this optimization was:
[Parallel(n_jobs=-1)]: Using backend LokyBackend with 8 concurrent workers.
[Parallel(n_jobs=-1)]: Done  34 tasks      | elapsed:  2.7min
[Parallel(n_jobs=-1)]: Done 150 out of 150 | elapsed: 10.9min finished
best params: {'c1': 0.08234416258689053, 'c2': 0.00019857762304671588}
best CV score: 0.9196892235606356
model size: 0.94M

hence, we got the best parameters by using 3 fold cross validation set..
Then the best model was prepared with the above parameters..


The result was:

              precision    recall  f1-score   support

          mr      0.926     0.998     0.961       454
          hi      0.892     0.937     0.914      1593
          te      0.725     0.996     0.839       519
          ta      0.853     0.974     0.910       543
          kn      0.851     0.995     0.918       598
          gu      0.538     0.989     0.697       185
          bn      0.903     0.988     0.944      1368
          ml      0.786     0.980     0.872       199
          en      0.953     0.750     0.840      3850

    accuracy                          0.881      9309
   macro avg      0.825     0.956     0.877      9309
weighted avg      0.897     0.881     0.880      9309


Hence, The accuracy jumped from 85.9% to 88.1% by hyperparameter optimization..

By further checking the report:

Top likely transitions:
en     -> en      2.310407
te     -> te      2.137228
bn     -> bn      1.999997
kn     -> en      1.410982
ta     -> ta      1.388948
mr     -> mr      1.332878
hi     -> hi      1.259815
kn     -> kn      1.193724
en     -> ta      1.115451
en     -> kn      1.014284
gu     -> gu      0.981621
ml     -> ml      0.979981
ml     -> en      0.889390
ta     -> en      0.875540
en     -> ml      0.770846
mr     -> en      0.714980
en     -> te      0.703097
te     -> en      0.617430
gu     -> en      0.550340
en     -> gu      0.496805

Top unlikely transitions:
ta     -> en      0.875540
en     -> ml      0.770846
mr     -> en      0.714980
en     -> te      0.703097
te     -> en      0.617430
gu     -> en      0.550340
en     -> gu      0.496805
bn     -> en      0.403851
hi     -> en      0.271526
en     -> mr      0.265183
en     -> hi      0.248853
en     -> bn      0.156480
ta     -> gu      -0.000020
hi     -> mr      -0.031734
bn     -> gu      -0.090501
hi     -> te      -0.222985
hi     -> gu      -0.295279
te     -> gu      -0.336079
bn     -> hi      -0.758866
hi     -> bn      -1.795771

#the below ones were booting the model score
Top positive: 
11.336704 hi       CurrentWord:tab
10.613269 en       CurrentLang:en
10.430693 en       CurrentWord:phone
10.104478 en       CurrentWord:movie
10.067667 en       CurrentWord:So
10.021286 en       CurrentWord:post
9.643074 en       CurrentWord:song
9.638517 en       CurrentWord:cinema
9.589696 en       CurrentWord:bomb
9.457883 en       CurrentWord:family
9.316024 en       CurrentWord:news
9.251741 en       CurrentWord:school
9.203305 en       CurrentWord:police
9.167212 en       CurrentWord:film
9.148515 en       CurrentWord:thanks
9.130408 en       CurrentWord:job
9.084101 en       CurrentWord:try
9.072153 en       CurrentWord:seat
9.070033 en       CurrentWord:Post
9.048087 en       CurrentWord:but
9.023156 en       CurrentWord:miss
9.008509 en       CurrentWord:weekend
9.001515 en       CurrentWord:star
8.989168 en       CurrentWord:room
8.931762 en       CurrentWord:sir
8.921783 en       CurrentWord:full
8.889428 en       CurrentWord:serial
8.848303 en       CurrentWord:video
8.842119 en       CurrentWord:dollar
8.834576 en       CurrentWord:plz

#the below ones are responsible for major downfall of model score
Top negative:
-5.397831 te       CurrentLang:hi
-5.413149 ta       NextWord:u
-5.415722 ta       PrevWord:in
-5.424467 ta       CurrentWord:Hi
-5.444010 hi       CurrentWord:male
-5.452353 ta       CurrentLang:hi
-5.481829 en       CurrentWord:aap
-5.543820 ta       NextWord:color
-5.571207 kn       CurrentLang:hi
-5.584091 en       CurrentWord:aapki
-5.608152 ta       NextWord:la
-5.639518 ml       NextWord:ne
-5.766589 ta       CurrentWord:th
-5.800410 ta       CurrentWord:and
-5.803793 ta       CurrentWord:Ha
-6.067884 en       CurrentWord:kai
-6.204091 ta       PrevWord:color
-6.453987 mr       NextWord:aste
-6.501662 ta       NextWord:e
-6.554021 ta       NextWord:Sir
-6.598479 ta       NextWord:le
-6.730581 ta       CurrentWord:Admin
-6.748180 bn       CurrentWord:min
-6.829639 en       CurrentWord:ki
-6.863888 hi       CurrentWord:Or
-6.914344 ta       CurrentWord:hi
-7.351551 kn       NextWord:na
-8.032762 ta       CurrentWord:Hero
-8.307760 hi       CurrentWord:nd
-8.578219 te       PrevWord:line


Then few more tweaks were done by carefully checking the report and the accuracy couldn't be improved 
more than 88.91% (that was the best this dataset could do without using lstm and other alogs)


