#Designing-Data-Intensive-Applications 

Load is described with a few numbers called Load Parameters.
Depending on your system, the best choice of the paramter can depend. Here are some examples:
	- requests per sec to web server
	- ratio of reads to writes in a database
	- number of simultaneously active users in a chat room
	- hit rate on a cache

## Example
---
An example from Twitter using data published in 2012.
Two of Twitter's main operations are
_Post Tweet_
	publish tweet to followers. (4.6k req/sec on average, over 12k req/sec at peak)
*Home timeline*
	User can view tweets posted by the people they follow. (300k req/sec)

The challenge is not handling 12,000 writes per second, but due to [[fan-out]] - each user follows many people, and each user is followed by many people. There are two ways of implementing this:
1) Posting a tweet simply inserts the new tweet into a global collection of tweets. When a user requests their home timeline, look up all the people they follow, find all the tweets for each of those users, and merge them (sorted by time). In a relational database, you could query like:
```
SELECT tweets.*, users.* FROM tweets

JOIN users ON tweets.sender_id = users.id

JOIN follows ON follows.followee_id = users.id 
WHERE follows.follower_id = current_user   
```
