# Recommendation_system
![image](https://user-images.githubusercontent.com/99672298/169068479-2d92e8ca-551e-4d50-9816-1964b0183885.png)

## Introduction
During the last few decades, with the rise of Youtube, Amazon, Netflix and many other such web services, recommender systems have taken more and more place in our lives. From e-commerce (suggest to buyers articles that could interest them) to online advertisement (suggest to users the right contents, matching their preferences), recommender systems are today unavoidable in our daily online journeys.

In a very general way, recommender systems are algorithms aimed at suggesting relevant items to users (items being movies to watch, text to read, products to buy or anything else depending on industries).

Recommender systems are really critical in some industries as they can generate a huge amount of income when they are efficient or also be a way to stand out significantly from competitors. As a proof of the importance of recommender systems, we can mention that, a few years ago, Netflix organised a challenges (the “Netflix prize”) where the goal was to produce a recommender system that performs better than its own algorithm with a prize of 1 million dollars to win.

In this article, we will go through different paradigms of recommender systems. For each of them, we will present how they work, describe their theoretical basis and discuss their strengths and weaknesses.

## Outline
In the first section we are going to overview the two major paradigms of recommender systems : collaborative and content based methods. The next two sections will then describe various methods of collaborative filtering, such as user-user, item-item and matrix factorization. The following section will be dedicated to content based methods and how they work. Finally, we will discuss how to evaluate a recommender system.

![image](https://user-images.githubusercontent.com/99672298/169068573-c84c1d50-b81d-4512-91b4-12cea9f624eb.png)
## Collaborative versus content
The purpose of a recommender system is to suggest relevant items to users. To achieve this task, there exist two major categories of methods : collaborative filtering methods and content based methods. Before digging more into details of particular algorithms, let’s discuss briefly these two main paradigms.

### Collaborative filtering methods
Collaborative methods for recommender systems are methods that are based solely on the past interactions recorded between users and items in order to produce new recommendations. These interactions are stored in the so-called “user-item interactions matrix”.

![image](https://user-images.githubusercontent.com/99672298/169069002-5ac7a2cf-fc76-4513-b838-5ee4f4a3c090.png)

Illustration of the user-item interactions matrix.
Then, the main idea that rules collaborative methods is that these past user-item interactions are sufficient to detect similar users and/or similar items and make predictions based on these estimated proximities.

The class of collaborative filtering algorithms is divided into two sub-categories that are generally called memory based and model based approaches. Memory based approaches directly works with values of recorded interactions, assuming no model, and are essentially based on nearest neighbours search (for example, find the closest users from a user of interest and suggest the most popular items among these neighbours). Model based approaches assume an underlying “generative” model that explains the user-item interactions and try to discover it in order to make new predictions.

![image](https://user-images.githubusercontent.com/99672298/169069170-0668b8e7-26ef-454d-845a-73254e2f6a64.png)

Overview of the collaborative filtering methods paradigm.
The main advantage of collaborative approaches is that they require no information about users or items and, so, they can be used in many situations. Moreover, the more users interact with items the more new recommendations become accurate: for a fixed set of users and items, new interactions recorded over time bring new information and make the system more and more effective.

However, as it only consider past interactions to make recommendations, collaborative filtering suffer from the “cold start problem”: it is impossible to recommend anything to new users or to recommend a new item to any users and many users or items have too few interactions to be efficiently handled. This drawback can be addressed in different way: recommending random items to new users or new items to random users (random strategy), recommending popular items to new users or new items to most active users (maximum expectation strategy), recommending a set of various items to new users or a new item to a set of various users (exploratory strategy) or, finally, using a non collaborative method for the early life of the user or the item.

In the following sections, we will mainly present three classical collaborative filtering approaches: two memory based methods (user-user and item-item) and one model based approach (matrix factorisation).

#### What is Collaborative Filtering?
Collaborative filtering is used by most recommendation systems to find similar patterns or information of the users, this technique can filter out items that users like on the basis of the ratings or reactions by similar users.

An example of collaborative filtering can be to predict the rating of a particular user based on user ratings for other movies and others’ ratings for all movies. This concept is widely used in recommending
movies, news, applications, and so many other items.

Let’s take one example and understand more about what is Collaborative Filtering,

let’s assume I have user U1, who likes movies m1,m2,m4. user U2 who likes movies m1,m3,m4, and user U3 who likes movie m1.

So our job is to recommend which are the new movie to watch for the user U3 next.

So here we can see users U1, U2, U3 watch/likes movies m1, so three have the same taste. now in user U1, U2 has like/watch movies m4, so user U3 could like movie m3 so I recommend movie m4, this is the flow of logic.

The key idea of CF is Users who agreed in the past tend to also agree in the future.

![image](https://user-images.githubusercontent.com/99672298/194805915-f2b1f8cd-fd51-43ef-a199-df254f16c1e6.png)

##### Types of Filtering
There are two types of Collaborative Filtering available:

+ **User-User-based similarity/Collaborative Filtering**
+ **Item-Item-based similarity/Collaborative Filtering**
+ **Note :**The most popular Collaborative Filtering is item-item-based Collaborative Filtering.

##### User-User-Based Collaborative Filtering
user-user collaborative filtering is one kind of recommendation method which looks for similar users based on the items users have already liked or positively interacted with. Let’s take a one eg to understand user-user collaborative filtering.

Let’s assume given matrix A which contains user id and item id and rating or movies.

![image](https://user-images.githubusercontent.com/99672298/194806072-10eb30bb-4ce6-4eb7-8b6b-060eac5efd79.png)

Compute a User User similarity follow these steps, so find a similarity between two users we can use cosine similarity.

so cosine similarity means the similarity between two vectors of inner product space, It is measured by the cosine of the angle between two vectors.

![image](https://user-images.githubusercontent.com/99672298/194806162-4246e47c-d2e5-4cb3-8903-0d8d78df4ba2.png)
![image](https://user-images.githubusercontent.com/99672298/194806209-5336679f-a2ee-4e31-9e2f-e51b4ab83198.png)

**So we find a similarity matrix here and our task is to recommend a new movie /item to a user.**

Suppose you have to recommend a new top 5 similar movie or item for a user 10, so we have a similarity matrix a and we go in a similarity matrix in user 10 and find a top 5 similar values corresponding to the user 10.

let’s suppose the top 5 similar to user10 is user 9,5,8,1,2. now you go into our user-item matrix and take all items of the user9,5,8,1,2 where they give a rating value and not watch by the user 10 and combine them. then we pick all those items and we recommended them for a user 10.

But there can be a small problem with a user-user similarity base system, user interests change over time, and then similarity values also change, and this is impacted on the recommended system.

##### There is another approach which is an item item-based similarity recommendation system.

#### Item-Item Based Collaborative Filtering

Let’s talk about Item-Based Collaborative Filtering in detail. It was first invented and used by Amazon in 1998. Rather than matching the user to similar customers, item-to-item collaborative filtering matches each of the user’s purchased and rated items to similar items, then combines those similar items into a recommendation list. Now, let us discuss how it works.

Item to Item Similarity: The very first step is to build the model by finding similarity between all the item pairs. The similarity between item pairs can be found in different ways. One of the most common methods is to use cosine similarity.

##### Prediction Computation: The second stage involves executing a recommendation system. It uses the items (already rated by the user) that are most similar to the missing item to generate rating. We hence try to generate predictions based on the ratings of similar products. We compute this using a formula which computes rating for a particular item using weighted sum of the ratings of the other similar products.

![image](https://user-images.githubusercontent.com/99672298/194806893-bca367f0-a725-4d9c-b396-aa4106c1a581.png)

**Example:
Let us consider one example. Given below is a set table that contains some items and the user who have rated those items. The rating is explicit and is on a scale of 1 to 5. Each entry in the table denotes the rating given by a ith User to a jth Item. In most cases majority of cells are empty as a user rates only for few items. Here, we have taken 4 users and 3 items. We need to find the missing ratings for the respective user.**

![image](https://user-images.githubusercontent.com/99672298/194806569-00bbbd44-f55d-4606-b676-ddb6c5fcbd08.png)
![image](https://user-images.githubusercontent.com/99672298/194806628-a8f1a22e-4894-49ae-a3fa-7315973ece09.png)
![image](https://user-images.githubusercontent.com/99672298/194806675-a87ad29c-0069-4e6d-9d6f-e1abb77bc054.png)
![image](https://user-images.githubusercontent.com/99672298/194806713-a2e9f826-13d0-432d-81d5-2b48d1e26854.png)

This is also very simple and very similar in idea with USER-USER Similarity Let’s dive deep into it.

This item-item similarity is solve a problem that occurs in a user user-based similarity.

Here we find a similarity matrix of items/movies, here we find a similarity between the two movies. to find a similarity we use a cosine distance between the two movies.

![image](https://user-images.githubusercontent.com/99672298/194807098-9a210ef5-a1d4-431f-b5c4-6be50a4b2a83.png)

**Simij= similarity(itemi , itemj)**

**So how to recommend an item to the user?**

Let’s suppose we have to recommend new items to user10, and we know a user10 already likes/watch item7,8,1. Now we go to the item-item similarity matrix, we take the most similar item to items7,8,1 based on the similarity values.

let’s suppose the most similar item for item7 is {item9, item4, item10}, the Most similar item to item8 is {item19, item 4, item10} and the Most similar item to item 1 is {item9, item14, item10}

Now we take a very common item from every set of items and the common items are {item9, item4, item10, item 19, item 14} and we recommend these all items to user10.

**The most popular filtering is item item-based filtering because over time item is not changed like the user user-based similarity.**

### Content based methods
Unlike collaborative methods that only rely on the user-item interactions, content based approaches use additional information about users and/or items. If we consider the example of a movies recommender system, this additional information can be, for example, the age, the sex, the job or any other personal information for users as well as the category, the main actors, the duration or other characteristics for the movies (items).

Then, the idea of content based methods is to try to build a model, based on the available “features”, that explain the observed user-item interactions. Still considering users and movies, we will try, for example, to model the fact that young women tend to rate better some movies, that young men tend to rate better some other movies and so on. If we manage to get such model, then, making new predictions for a user is pretty easy: we just need to look at the profile (age, sex, …) of this user and, based on this information, to determine relevant movies to suggest.

![image](https://user-images.githubusercontent.com/99672298/169069230-1b0a43be-3c16-4b6d-ab45-eb1389ccd8fc.png)

Overview of the content based methods paradigm.

<span style="color:blue">Content based methods suffer far less from the cold start problem than collaborative approaches: new users or items can be described by their characteristics (content) and so relevant suggestions can be done for these new entities.</span> Only new users or items with previously unseen features will logically suffer from this drawback, but once the system old enough, this has few to no chance to happen.

Later in this post, we will further discuss content based approaches and see that, depending on our problem, various classification or regression models can be used, ranging from very simple to much more complex models.

### Models, bias and variance
Let’s focus a bit more on the main differences between the previously mentioned methods. More especially let’s see the implication that the modelling level has on the bias and the variance.

In memory based collaborative methods, no latent model is assumed. The algorithms directly works with the user-item interactions: for example, users are represented by their interactions with items and a nearest neighbours search on these representations is used to produce suggestions. As no latent model is assumed, these methods have theoretically a low bias but a high variance.

In model based collaborative methods, some latent interaction model is assumed. The model is trained to reconstruct user-item interactions values from its own representation of users and items. New suggestions can then be done based on this model. The users and items latent representations extracted by the model have a mathematical meaning that can be hard to interpret for a human being. As a (pretty free) model for user-item interactions is assumed, this methods has theoretically a higher bias but a lower variance than methods assuming no latent model.

Finally, in content based methods some latent interaction model is also assumed. However, here, the model is provided with content that define the representation of users and/or items: for example, users are represented by given features and we try to model for each item the kind of user profile that likes or not this item. Here, as for model based collaborative methods, a user-item interactions model is assumed. However, this model is more constrained (because representation of users and/or items are given) and, so, the method tends to have the highest bias but the lowest variance.

![image](https://user-images.githubusercontent.com/99672298/194988514-a2294d05-8547-4ca6-8c16-3f958f26b387.png)
![image](https://user-images.githubusercontent.com/99672298/194988552-9a8c87d7-4b42-4b90-9d2c-8d5ed45df7b3.png)
![image](https://user-images.githubusercontent.com/99672298/194988694-0c829b0a-6eb8-4e90-9115-b2a58ccfeeeb.png)
![image](https://user-images.githubusercontent.com/99672298/194988789-7e11b37c-8654-4838-9274-9ba86462b924.png)
![image](https://user-images.githubusercontent.com/99672298/194988829-13531c90-313c-411b-818d-3f7b75ac5bd4.png)


## Author

<table>
<tr>
<td>
     <img src="https://avatars.githubusercontent.com/u/99672298?v=4" width="180"/>
     
     moindalvs@gmail.com

<p align="center">
<a href = "https://github.com/MoinDalvs"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
<a href = "https://twitter.com/DalvsHubot"><img src = "https://www.shareicon.net/download/2016/07/06/107115_media.svg" width="36" height="36"/></a>
<a href = "https://www.linkedin.com/in/moin-dalvi-277b0214a//"><img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/></a>
</p>
</td>
</tr> 
  </table>
