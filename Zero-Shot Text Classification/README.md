# W2V-based Zero-shot Text Classification


The code for this challenge is contained in the iPython Notebook Zero-Shot Text Classification.ipynb. The code is all commented, and the cell outputs should all still be visible.


## To Re-Run (not necessary to view results):

1. Install the requirements listed in requirements.txt
2. Execute the code blocks in order. Note that the last 2 sections "Architecture 1 Parameter Search" and "Retrain Full Model with Best Parameters" take several hours to execute if you are not using a GPU. These are out of the required scope of the assignment, but I thought it would an interesting experiment.
3. You can save the results of the data processing to save time for future testing by uncommenting the save data lines in the first block after Architecture 1. You can load the saved data in using the other lines in the same block.


## Overview of My Process:

Loading Data:
I first extracted the embeddings from GoogleNews-vectors-negative300.bin, and created a pandas dataframe containing the dataset's text and labels.


Averaging Word Embeddings:
I tokenized each sentence, and averaged the word embeddings for each token in the the sentence. In doing this, I realized that some tokens did not have embeddings, so I kept track of the sentences which only contained tokens without embeddings and eliminated them from the dataset.


Clustering and PCA:
I first used PCA to visualize the averaged embeddings then ran a KMeans clustering with 2 centroids and plotted the results. It was very dense with points at first so I shuffled the embeddings and took 1/6th of the dataset to get a better sense of the clustering. 


Mapping Keywords to Embeddings:
I created a dictionary where each keyword is mapped to a PyTorch tensor representation of the GoogleNews embedding.


Concatenating Text and Keyword Embeddings:
For each keyword associated with a sentence, I concatenated that sentence's averaged embedding with the embedding for the keyword. For each positively associated keyword, I also concatenated the sentence with a negatively associated keyword to balance the number of positive and negative examples.


Processing with Neural Network:
I split the data into 90-10 train/test and created a PyTorch DataLoader for training. I used a neural network with 4 dense hidden layers of size 600, 1000, 500, and 100 which feed into a single output neuron with a sigmoid activation for binary classification. These parameters were honestly just a first guess, but it ended up working very well because after training it had an accuracy of 93 percent. Note: I originally used SGD with momentum, but Adam seemed to perform slightly better, so I stuck with that for all further tests.


Parameter Search:
Even though my first try worked well, I wanted to see if I could do better, so I varied certain parameters (2 hidden sizes of dense layers, batch size, and implementing dropout) in various combinations. I then performed a parameter search on 4 folds, averaged the accuracies, and saved the results in a dictionary.


Retrain Model:
I retrained a model using the best parameters found from the parameter search, and ended up with a similar accuracy as my initial run. This isn't all that surprising as the best results from the parameter search were only marginally better. To try and further improve performance, I think I would have to vary the architecture more significantly as the 4 dense layers may have maxed out their potential.

I would try implementing an LSTM module before the dense layers and feed in the word embeddings concatenated with the keyword embedding one at a time (as opposed to an average of the words in the sentence). I would also try transformer based architectures like BERT or a CNN-based architecture like U-net or RESNet (although I'm not very confident how this would work on text data but I'd give it a shot).


