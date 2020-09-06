# Ratings
You need be consistent when providing ratings data. You can't have items rated on a 0-5 scale, and other items rated on a 0-100 scale.

You can keep it simple. Only collect ratings on, say, a 0-5 scale throughout your platform. 

If you insist on using different scales, you need to normalize the ratings before submitting them to the SimpleRecommend API. How you choose to do so does not matter, as long as all ratings are submitted within the same range. This range, your decided minimum and maximum rating, also needs to be set in your Recommendation settings.

## Explicit vs. Implicit Ratings
The most obvious ratings are, well, explicit. You ask users to give a product 0 to 5 stars and they make their choice. 

You can also gather implicit ratings by tracking the user behaviour on your site. This is beneficial for building a greater dataset, however, it's much trickier to work with. First, you have to determine what actions to track, how to interpret them and their indication of an user's preferences, and how to quantify the ratings.

We can't give a clear-cut answer specific to your platform. However, one simple way is make use of binary implicit ratings. When a user has not or has bought or viewed an item. In that case, you would *only* need to create Events when an Actor has, say, bought something, with an arbitrary rating value such as 1. SimpleRecommend will still find patterns and generate specifications.

