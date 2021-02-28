# Email Clustering

Simon Gilbert
simonsai@bu.edu

## Running This Notebook

To run, make sure that the folder 'Data' is in the same working directory as 'Email Clustering.ipynb'

## Approach

This problem immediately stuck out to me as one that could be solved with a clustering algorithm. I chose K-Means because it is reliable and easy to implement.

The next step was choosing what part of the data to focus on. The given email corpus has a lot of variation in terms of what information is given for each email. I chose to only utilize the email-body text for the K-Means clustering (see Future Work section). Once the data were loaded in, I cleaned it by eliminating everything but the English words contained in the NLTK words.words() corpus. This choice eliminated a lot of names, URLs, misspelled words, and numbers which, given more time, would be interesting to analyze, but I kept it to common English words for this challenge. 

The next decision I had to make was how I wanted to view the results of the algorithm. I decided to use the term frequency–inverse document frequency (TF-IDF) metric which indicates how important a word is to the body from which it is pulled. I chose this because it has a host of NLP application and was simple to implement given how the data were structured.

To perform the clustering, I first did a principal component analysis (PCA) to better visualize the distribution of the data. Plotting this revealed that the data distribution was shaped like a 3-pronged blob which looked like it could cluster easily into 3 groups. Running K-Means accomplished exactly that; the blob separated into 3 relatively neat clusters. 


## Analysis of Results

I found the top 25 words in each of the 3 clusters as determined by their TF-IDF score, and printed that information in the jupyter notebook. All 3 groups have similar terms in them, all pertaining to business-type things: "date, schedule, meeting, conference, company, message,...". 

I couldn't parse exactly how the clustering algorithm defined its boundaries, but I think that may be a result of how the data are distributed. As mentioned above, PCA found that the data take the form of a 3-pronged blob. However, when the clusters are formed, most of the data points lie close together at the center of the cluster. This could explain why there is so much overlap between the top words in all 3 groups and why it's difficult to figure out exactly what defines the clusters. There are points farther from the blob's center which would be interesting to explore, but I didn't have time to really dive into that.


## Future Work

For loading in the data, my original plan was to use additional information for clustering other than just the email-body: namely who the sender/recipients were. I feel like this could lead to some additional insights about how the data are distributed and how they might cluster, but I did not have the time to implement it for this challenge.

Another metric I would like to test is word frequency as opposed to TF-IDF. I think it's possible that the clustering might make more sense with a simpler metric. That or I would research other NLP metrics to find one most appropriate to this problem. 

## Final Notes

Thank you for this opportunity! Regardless the outcome of your decision, I would appreciate some feedback on how I did on this challenge and what I could do to improve for the future.

Hope to hear from you soon.


