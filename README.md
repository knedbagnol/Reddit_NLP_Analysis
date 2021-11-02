# Project 3, NLP and Me
##### Kennedy Bagnol
___

## Problem Statement
___
Can I create a model that can differentiate between posts from r/AskMen and r/AskWomen? These two subreddits are targeted at asking women and men questions and expanding the perspective of all readers with the answers of various people from the subreddit. Creating a model to differentiate the two subreddits will shed a light on how different the questions from each subreddit are and will hopefully lead to a better understanding of how we perceive men and women in our society. 

## Executive Summary
___
The difference between men and women has always been a big topic of conversation throughout the history of humanity. Because of this, today's society tends to view men and women pretty differently. This can be seen in our mass media, news reporting, and in our everyday conversations. 

There are two subreddits that allow us to see this difference in real time. r/AskMen and r/AskWomen. The idea behind these subreddits is that people ask men and women different questions. A pretty simple concept, but looking at each subreddit can tell us a lot about the perceived diffrences between men and women (at least the ones on reddit).

With this project I wanted to see how different the questions people ask men and women are. The idea being, that the more different the questions asked are, the higher score my models would get on the testing data. And if they are more similar, then our model will have a harder time discerning which post came from which subreddit. 

I will be looking at 1,000 posts from the top of this past year from each subreddit for a total of 2,000 documents in our corpus. Since the data pull is 50/50 from each subreddit, our baseline is 50%. 


## Data Dictionary for the scraping
| Column    | Description                      |
|-----------|----------------------------------|
| Title     | The title of the post            |
| Subreddit | The subreddit the post came from |
| Selftext  | The body text of the post        |

___

## Results of Models
| Model             | Training Score | Testing Score | Best Score | AUC |
|-------------------|----------------|---------------|------------|-----|
| CVec MNB (Sent)   | .86            | .78           | .77        | .86 |
| CVec MNB          | .88            | .76           | .78        | .86 |
| CVec KNN          | .75            | .64           | .66        | .70 |
| Tf-Idf MNB (Sent) | .88            | .78           | .79        | .87 |
| Tf-Idf MNB        | .87            | .79           | .80        | .88 |
| Tf-Idf RF         | .80            | .78           | .80        | .85 |
| Tf-Idf DT         | .85            | .76           | .79        | .82 |
| Tf-Idf SVM        | .99            | .79           | .81        | .89 |
| Tf-Idf LogR       | .80            | .76           |            | .88 |
| Tf-Idf LinR       | .22            | .25           |            |     |

## Conclusions   
There was not as much of a difference between the models as I thought there would be. I believed SVM would be significantly higher than the rest. Although it had a ridiculously high training score, the testing score was very similar to the rest (it did have the highest AUC, but only by .01). All of the models being similar makes me think that the subreddits are decently different in content, but also have a small amount of overlap
___
From a cursory glance, the top questions in AskWomen seem to be more serious than the top questions in AskMen. However they do have a decent overlap in relationship questions and that is where I believe the model struggles to classify the most.

___
Overall, I would say that our model was decently successful in it's goals. Additionally, this was a relatively simple model that didn't really take into account the context of the post and used a Bag-of-Words approach. I think what this model can tell us though, is that we generally ask pretty diferent questions between men vs women. This makes sense when taking into consideration society's different views on men vs women, and is exemplified by the difference in the topics of the top posts from each subreddit. 
​
___
## Recommendations  

For future modeling I would start by using an aggregated model to combine all of our models and hopefully generate a better score than any one model individually. Additionally I would like to be able to pull even more posts from the subreddit. Part of the reason why I believe most of the models were overfit is because there were words in the testing set that were not in the training set, therefore the model had no idea what to do with some testing set values as they had never seen some of the features before. This can be solved by increasing the size of our data so hopefully there is more overlap between the training and testing data features. I think it would also be good to do more focused stop word removal for a deeper level of feature engineering.

# Future Exploration

I think there are a couple directions this project could go in:

1: Do a more in depth sentiment analysis/classification of each subreddit. Does a certain subreddit have more relationship oriented questions? Does one have more jo
ke posts than the other? It would be cool to map out the different types of posts in each subreddit.

2: Explore the comments section. Does one subreddit tend to agree with eachother more than the other? Do certain types of posts garner more interaction than other types of posts? Comments are the other half of the coin on Reddit, so I think it would be good to explore. 

## Sources
---
1. **Reddit**
    1. [Reddit](https://reddit.com)
    2. [r/AskWomen](https://www.reddit.com/r/AskWomen/top/?t=all)
    3. [r/AskMen](https://www.reddit.com/r/AskMen/top/?t=all)
1. **PRAW** - Python Reddit API Wrapper
    1. [Youtube Tutorial](https://www.youtube.com/watch?v=8VZhog5C3bU&ab_channel=PythonEngineer)
    2. [Praw Documentation](https://praw.readthedocs.io/en/stable/)
1. **Etc.** various sources of information
    1. [Machine Learning] (https://towardsdatascience.com/machine-learning-text-processing-1d5a2d638958)
    2. [DataFrame.apply] (https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html)
    3. [Stemming in Nltk] (https://machinelearningknowledge.ai/beginners-guide-to-stemming-in-python-nltk/)
    4. [Merging Data] (https://datacarpentry.org/python-ecology-lesson/05-merging-data/)
    5. Lessons: 4.07, 5.-, 6.-