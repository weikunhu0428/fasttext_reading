[link](http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)

Train a simple neural network with a single hidden layer to perform a certain a task, but we are not actually going to use the neural network for the task. The goal is to learn the weights of the hidden layer, which is the word vector.

We will train a neural network that given a word in the middle of a sentence (input word), look at the words nearby and pick one at random. The network provides the probability for every word in the vocabulary of being the nearby word that we chose. When I say "nearby", there is actually a "window size" parameter to the algorithm. A typical window size might be 5, meaning 5 words behind and 5 words ahead (10 in total).

The output probabilities are going to relate to how likely it is find each vocabulary word nearby input word. For example, if you gave the trained network the input word “Soviet”, the output probabilities are going to be much higher for words like “Union” and “Russia” than for unrelated words like “watermelon” and “kangaroo”. We’ll train the neural network to do this by feeding it word pairs found in our training documents. The network is going to learn the statistics from the number of times each pairing shows up.

There is no activation function on the hidden layer neurons, but the output neurons use softmax. When training this network on word pairs, the input is a one-hot vector representing the input word and the training output is also a one-hot vector representing the output word. But when you evaluate the trained network on an input word, the output vector will actually be a probability distribution (i.e., a bunch of floating point values, not a one-hot vector).

For our example, we’re going to say that we’re learning word vectors with 300 features. So the hidden layer is going to be represented by a weight matrix with 10,000 rows (one for every word in our vocabulary) and 300 columns (one for every hidden neuron).

300 features is what Google used in their published model trained on the Google news dataset (you can download it from here). The number of features is a "hyper parameter" that you would just have to tune to your application (that is, try different values and see what yields the best results).

The 1 x 300 word vector for “ants” then gets fed to the output layer. The output layer is a softmax regression classifier. There’s an in-depth tutorial on Softmax Regression here, but the gist of it is that each output neuron (one per word in our vocabulary!) will produce an output between 0 and 1, and the sum of all these output values will add up to 1.

Specifically, each output neuron has a weight vector which it multiplies against the word vector from the hidden layer, then it applies the function exp(x) to the result. Finally, in order to get the outputs to sum up to 1, we divide this result by the sum of the results from all 10,000 output nodes.

Note that neural network does not know anything about the offset of the output word relative to the input word. It does not learn a different set of probabilities for the word before the input versus the word after.

If two different words have very similar “contexts” (that is, what words are likely to appear around them), then our model needs to output very similar results for these two words. And one way for the network to output similar context predictions for these two words is if the word vectors are similar. So, if two words have similar contexts, then our network is motivated to learn similar word vectors for these two words! 
