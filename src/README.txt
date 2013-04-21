	CSE223B Lab2
	Jian Xu, A53026658
	jix024@eng.ucsd.edu


********	HOW TO RUN	********

Simply run make, and start the server. You can use the tribble_client or web application to test it.


********	EXPLAINATION      ********

Tribble_server.cpp:

This file includes all the methods that communicate with client and abcking server.

CreateUser():
First use Get(userid) to check if the user exists.
If the userid already exists, return OK; otherwise use Put(userid, "Created") to backing store server. if Put returns OK, return OK to client, otherwise return error.

AddSubscription():
First check if both the userid and subscribeto exists.
Then add subscribe to userid_sublist list and make sure it succeed.

RemoveSubscription():
First check if both the userid and subscribeto exists.
Then remove subscribe from userid_sublist list and make sure it succeed.

PostTribble():
First check the userid exists.
Then format the tribble as {{userid},{tribble content}} pattern.
Get the current timestamp, add the tribble pattern to timestamp list, then add the timestamp to user_tribbles list.
This makes sure we do not get a long list of all tribbles in a GetList(). Instead, we get the timestamps list, then retrieve the tribble from the timestamp list.

GetTribbles(): 
First check the userid exists.
Then get the timestamp list from user_tribbles list, then retrieve the tribble from the timestamp list. Return when we get 100 tribbles.

GetTribblesBySubscription():
First make sure the userid exists.
Then by calling GetSubscriptions(), get the subscription list.
Then for each subscription in the list, use GetTribbles() to get the tribbles, then group the list and return the latest 100 tribbles.

GetSubscriptions():
First make sure the user exists.
Then get the subscriptions by GetList(user_subscribe).


