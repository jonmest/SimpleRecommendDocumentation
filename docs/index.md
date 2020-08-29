# Welcome to SimpleRecommend's documentation!

SimpleRecommend is a service for you who want to generate customized recommendations for website users. We have developed a dynamic machine learning system that finds patterns in your users' preferences and recommends items similar to what they historically have preferred. 

> Our leading goals are simplicity and flexibility, to allow any business to supercharge their business with AI at a low cost.

For these reasons, there are compromises that have to be acknowledged. The dynamic, general nature of our recommendation engine will possibly mean it will be less accurate than a bespoke, in-house developed engine built specifically for your userbase's behaviours.

However, with SimpleRecommend you get rid of all the headaches of developing such an engine, and you could save hundreds of thousands of dollars from not having to hire a team of machine learning experts.

## Possible Benefits Of A Recommendation Engine
Recommender engines are systems that aims to predict the preferences of a user, and they are primarily used in commercial applications.

Netflix, YouTube and Spotify are all companies that spend vast resources on developing their recommendation engines, since it is simply so beneficial to their business. Providing custom recommendations to users can give you several possible benefits:

- Improve conversion rates
- Increase average order value
- Enhance the user experience and consequently your brand value

Obviously, none of these are guaranteed. Our goal is to make SimpleRecommend a simple, hands-off engine, but in the end you will still have to perform some kind of testing to determine if it makes sense economically for your business.

## How SimpleRecommend Generates Recommendations
SimpleRecommend utilizes a type of algorithms called item-based collaborative filtering, which was first invented by the ecommerce company Amazon. To explain it as a simple as possible, it can be likened to:

"Persons who rate item X highly, such as you, also tend to rate item Y highly. You haven't rated item Y yet, so you should try it".

Despite its simplicity, this technique is generally more accurate than other popular recommendation algorithms, and more efficient to compute, which is one of the reasons we can provide access to SimpleRecommend at such a low price.

## Key Concepts
---
To understand SimpleRecommend you need to be familiar with a few concepts.

### Provider
When using SimpleRecommend, you are a Provider. All users and user data tracked will be tied to your Provider ID.

### Actor
Your customers, users -- what have you -- become Actors when you attempt to track their preferences and generate recommendations for them.

### Item
An item is anything you want to recommend. If you run an ecommerce store, this will be your products. If you run a blog, it may be your blog posts. When interacting with SimpleRecommend, each of your Items need to have an unique ID. When eventually fetching recommendations, you receive a list of recommended item IDs.

### Rating
A rating is an indicator of a Actor's liking of an Item. You need to set a minimum and maximum rating in your recommendation settings, and they have to be different from one another. Other than that, the ratings can be in any format as long as they are consistent. In ecommerce stores, for example, this may be a scale from 0-5 stars, or a binary scale from 0 to 1 to symbolize a thumbs up or down.

### Event
To supply data our machine learning model can base its recommendations off of, you need to create Events. An Event is a JSON object describing something an Actor has done and it contains three crucial pieces of data.

- The Actor's ID
- The relevant Item's ID
- The Rating (what did the Actor rate the Item?)

## Basic workflow for generating recommendations
After you've created and activated your SimpleRecommend account, there are a few things you need to do in order to start generating recommendations for an user.

Let us assume you run an ecommerce store:

### 1. Create an Actor
You have an user, Bob, and want to start learning his preferences. The first thing you'll have to do is to create an Actor. You don't have to provide any of the user's data to us. You just send a request to create a new Actor, and receive a token in the response.

You will then have to store and associate this token with the user Bob. How to do that is up to you. You could store it as a cookie in the user's browser, or in your database. We don't care as long as you can provide this token in future exchanges with us.

### 2. Create Events
When Bob buys a product in your store, you have decided to consider that an indicator of his preferences. Thus, you want to use this information to recommend other items Bob may like.

Every time Bob purchases an product, you post a request to us:
```
{
    "actor": "BobsActorToken",
    "item": "TheItemHeBoughtID",
    "rating": 1
}
```
If the rating of "1" in the example above confuses you, we recommend you read the various guides on ratings in this documentation. Right now, the important thing is understanding this is what you'll need to send us so we can model an user's preferences.

### 3. Request recommendations
After you've created at least two Events for one specific Actor, recommendations will start to be generated for them. They're unlikely to be very appealing to the Actor at such an early point, but tend to get more tailored to the Actor's preferences over time as more data builds up (a rule of thumb is, that the more data, the better).

Send us a GET request:
```
GET /recommendations/actor={BobsActorToken}
```
To receive a JSON object in this format:
```
{
    "items": [
        "recommendedItem1ID",
        "recommendedItem2ID",
        "recommendedItem3ID",
    ]
}
```

## Security and authentication
In the world of recommendation engines, there is an issue of malicious parties attempting to "taint" a websites user data in order to make the recommendations less accurate. To mitigate this, you will have to whitelist one or several hostnames in your SimpleRecommend account settings. When sending requests to the API the origin has to be whitelisted. A hostname is simply the domain name or IP adress from which the request originates. If the origin of a request does not match with a hostname that is whitelisted, the request will receive a 401 status code in response.

### API key
You can also opt-in to having to authorize every request with a secret API key. However, this is only worthwhile if all your requests to the SimpleRecommend API will be sent from your backend servers, as the client should always be considered insecure. Taking this security measure ensures better integrity of your user data, albeit being less convenient at times.

### Shilling attacks
Please note, that your data can still be manipulated to reduce recommendation quality. "Shilling attacks" is a type of manipulation where a malicious party injects around 1-5% the size of your user base with fake profiles. In reality, there is not terribly much that can be done about such attacks, and the area of recommendation systems is still very much under development. However, you can mitigate it by attempting to detect spam users, and only sending Events for registered, verified users. Additionally, the type of recommendation algorithm SimpleRecommend utilizes, item-based collaborative filtering, is slightly more robust to these attacks than other popular algorithms.