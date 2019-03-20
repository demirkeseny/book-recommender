# Recommending Your Next Book

> Author: Yalim Demirkesen | [github.com/demirkeseny](github.com/demirkeseny)
>
> Presentation: [Google Slides](https://docs.google.com/presentation/d/1fCGsQedn6SWS13BpRvaHgE5fWb5YCHEmzU9DHsPIhTg/edit?usp=sharing)
>
> Date: March 2019



## Problem Statement

If you are a book worm, you might spend more time deciding what to read next than reading the book itself. In social media, there are lots of sources that recommend us what to read next. These are usually based on other users' preferences or the average rating of the books. This is a nice approach for mainstream books but if we want to have a more personalized recommendation, we might approach this from another perspective. Maybe my recommendation engine can do the task of *Recommending Your Next Book*!  

<img src="C:\Users\demir\OneDrive\GA\DSI_6\Projects\book-recommender\images\t1.PNG" width="400px">



## Objective

The goal of this project is to build a recommendation engine that can suggest next books based on user ratings or similarity in the book descriptions. For that purpose, I built different models that can create a recommendation on user-based, item-based and content-based.



## Understanding the Recommender Systems

While making a recommendation there are two methods that can be applied. First one is the collaborative filtering. In this case, we take into account the user ratings. From the user ratings, we can either find similar users and then predict what the target user would vote for a certain book based on the ratings of other similar users or we can recommend books with similar contents. 

### Collaborative Filtering

In the collaborative filtering we need to have a good amount of user ratings. These ratings are used to understand the most similar users. We can measure the similarity by considering each user as a vector in the space. The direction and magnitude of each vector is calculated considering the user ratings. 

From this point, we can measure the similarity between the users by **cosine similarity**. The less cosine similarity is, more similar two users get. After we label similar users, we can predict how one of those similar users will vote a certain book. 

![title](https://github.com/demirkeseny/book-recommender/blob/master/images/CF.PNG)

From the above image we see two users. They read the books on the left hand side. Considering their ratings to these books, we label them as similar users. Then the first user reads *The Great Gatsby* and rates it with a good score. Since these two users have similar taste, recommendation engine suggests this book to the second user. 

### Content-Based

Content-based recommendations are the second type of recommender systems. These usually take into account the similarity in the contents of each item. In our case, I created an NLP model to measure the similarities between the book descriptions. I measured the word frequencies in each description and measured the similarities between books. 

![title](https://github.com/demirkeseny/book-recommender/blob/master/images/CB.PNG)

From the above image, we can see a user reading *Troy*. (S)he rates it highly. Our recommendation engine runs the NLP model and finds out the similar contents as *Troy*, which is *SPQR* in our example. *SPQR* is suggested to the user considering that (s)he will enjoy this one too since it has a similar content as the first book.

## Data

## Models 

## Future Developments

## Change the pic locations to url









