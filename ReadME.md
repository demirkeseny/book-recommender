# Recommending Your Next Book

> Author: Yalim Demirkesen | [github.com/demirkeseny](github.com/demirkeseny)
>
> Presentation: [Google Slides](https://docs.google.com/presentation/d/1fCGsQedn6SWS13BpRvaHgE5fWb5YCHEmzU9DHsPIhTg/edit?usp=sharing)
>
> Date: March 2019



## Problem Statement

If you are a book worm, you might spend more time deciding what to read next than reading the book itself. In social media, there are lots of sources that recommend us what to read next. These are usually based on other users' preferences or the average rating of the books. This is a nice approach for mainstream books but if we want to have a more personalized recommendation, we might approach this from another perspective. Maybe my recommendation engine can do the task of *Recommending Your Next Book*!  

![tweet](https://github.com/demirkeseny/book-recommender/blob/master/images/t1.PNG | width = 48)


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

To build this sort of recommender system, we need a good amount of user ratings and book information. That can be obtained from [goodreads.com](www.goodreads.com) which is the most extensive book database available online. On this webpage, there is a book list called *[Best Books Ever](https://www.goodreads.com/list/show/1.Best_Books_Ever)*. Although there are more than 55,000 books on this list, 10,000 of those are provided on [Kaggle.com](https://www.kaggle.com/zygmunt/goodbooks-10k), which is an enough amount for our purpose. This dataset includes also the user ratings for each of those 10,00 books.

Although this dataset is extensive, we are still lacking some content information. There, I benefit from the [goodreads module](https://github.com/sefakilic/goodreads). This module, provides a detailed description about each book. One limitation is that some books don't have any description, which are excluded form analysis.



## Models 

For this project I have built three models:

### Collaborative Filtering - Item Based

In item based collaborative filtering, I used the user ratings for each book and then calculated the similar books. The user is able to input a book name and the recommendation engine generates similar kind of books based on user ratings. 



For instance when *Lost Symbol* by *Dan Brown* is entered to the model, the model generates the following ten recommendations:



| Similarity Index | Book Name                             |
| ---------------- | ------------------------------------- |
| 1                | Digital Fortress                      |
| 2                | Deception Point                       |
| 3                | Inferno                               |
| 4                | The Girl who Kicked the Hornet's Nest |
| 5                | Eclipse                               |
| 6                | The Runaway Jury                      |
| 7                | A Dance with Dragons                  |
| 8                | New Moon                              |
| 9                | Breaking Dawn                         |
| 10               | The Da Vinci Code                     |



### Collaborative Filtering - User Based

For the user based collaborative filtering I used the module called [Surprise](http://surpriselib.com/). This was a very useful module to generate recommendations in a faster way. After running multiple algorithms, I ended up with SVD as the most optimal solution. SVDpp had a better test score but decided to pick SVD since it runs almost eight times faster than SVDpp.



For the user `12874`, we can see the recommendations as below:



| Similarity Index | Book Name                               | Actual Rating | Estimated Rating |
| ---------------- | --------------------------------------- | ------------- | ---------------- |
| 1                | The Return of the King                  | 4.0           | 4.0              |
| 3                | The Giving Tree                         | 4.0           | 3.9              |
| 4                | The Hobbit Bookset                      | 4.0           | 3.9              |
| 2                | A Light in the Attic                    | 4.0           | 3.9              |
| 5                | Roots: The Saga of an American Family   | 4.0           | 3.9              |
| 6                | Green Eggs and Ham                      | 4.0           | 3.8              |
| 7                | Philosopher's Stone                     | 4.0           | 3.8              |
| 8                | The Art of Racing in the Rain           | 4.0           | 3.8              |
| 9                | A Wrinkle in a Time                     | 4.0           | 3.7              |
| 10               | Hotel on the Corner of Bitter and Sweet | 4.0           | 3.7              |



### Content-Based Recommendation

On content based recommendations, I used the book descriptions. The similarities between all is measured by Count Vectorizer. More frequent a group of words is, higher the similarity gets between books.

 

In order to test that I searched for the book *Treasure Island*:

| Similarity Index | Book Name                         |
| ---------------- | --------------------------------- |
| 1                | Treasure Island (Famous Five, #1) |
| 3                | The Black Arrow                   |
| 4                | The Count of Monte Cristo         |
| 2                | The Dark is Rising Sequence       |
| 5                | The Complete Sherlock Holmes      |
| 6                | The Thief                         |
| 7                | Low Country                       |
| 8                | The Reed                          |
| 9                | Inca Gold                         |

From the table it is possible to say that we have a similar genre or content selection as *Treasure Island* but for instance the first recommendation is a completely different type of book, genre and author but since the name of the books are similar, it is very misleading. 



## Evaluation

Only for user based collaborative filtering, evaluation makes more sense since we have a predicted scores and we can compare them with actual results. The evaluation metric that I used was RMSE.

![title](https://github.com/demirkeseny/book-recommender/blob/master/images/act_vs_pred.PNG)

In the above graph we can see what we predicted using SVD vs what is the actual rating of our target user for each book.

## Future Developments

This project has a big potential to grow since recommendation engines can always be more accurate but in specific there are couple of steps I might perform in the future to take this project to the next level:

- There might be an hybrid model that combines my three models. 
- The number of books and users can be extended. In order to do that, I need to scrape goodreads with my own scraper which is more complicated.
- If all the books can be loaded to the NLP model as PDF files, it could make more sense to run the Count Vectorizer.











