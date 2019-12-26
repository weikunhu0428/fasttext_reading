
fastText is on par with deep learning classifiers in terms of accuary, and many orders of magnitude faster for training and evaluation.

The fastText model could be trained in less than ten mins with more tha one billion words using a standard multicore CPU, and classify half a million sentences among 312K classes in less than a minutes.Text Classifiction is an important task in Natural Language Processing. 

Linear classifiers are considered as strong baselines for text classifcation problem, which could reach high performance if right features are selected. Downside for the exsiting models are slwo and scale to large corpus.

Simple and efficient baseline for __sentence classifcation__ is to represent sentences as bag of words and train a linear classifier (logsitics regresssion of an SVM). However, linear classificers do not share parametes among features and classes, which limits the generalization in the context of large output space where some classes have very few examples. (common solutions is to factorize the linear classifer into low rank matrics or use multilayer neural networks)

__N-gram__ feature: bag of words is invariant to word order but taking word order into account is often computationlly expensive. Instead, we use a bag of n-grams as additional features to capture some partial information about the local word order. This is efficient in practice while achieving comparable results to methods taht use the order.

The fast and memory efficent mapping of the n grams could be achived by using hashing trick with same hashing function in [Mikolov (2011)](https://www.researchgate.net/profile/Lukas_Burget/publication/241637478_Strategies_for_training_large_scale_neural_network_language_models/links/542c14960cf27e39fa922ed3.pdf) and 10 M bins iwth bigrams, and 100M otherwise.





