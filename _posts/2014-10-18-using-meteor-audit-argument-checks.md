---
layout: post
title: using meteor audit-argument-checks
---

##About Meteor
[Meteor](https://www.meteor.com/) is an open-source platform for building web apps. It is a full stack javaScript platform  built on top node.js. Meteor is easy to learn and yet powerful.
Meteor uses JavaScript on both the client and on the server. 

##what is audit-argument-checks ? 
It is a meteor package which throws an Meteor.Error when we are using client  side data without validating it.  ( Never trust a user input. right? ). Its job is to enforce security checks. For some weird reason many developers are not using it.

{% highlight javascript %}
meteor add audit-argument-checks
{% endhighlight %}

simply pass values comes from client side and their data types in to check().

{% highlight javascript linenos %}
  Meteor.methods({
    DeleteUser: function(userId, userName) {
      check(userId, String);
      check(userName, Match.Any);
      //rest of the code
    }
  });
{% endhighlight %}

###Important
* If you forgot to validate userId and userName on server side It will simply give a server side warning but it will not stop executing your code.
* If you use check() and it if client inputs doesnot match with your expected format it will throw a Error and it will not executed the code further.

If you are interested in learning more about audit-argument-checks we should checkout [Bullet one of BulletProof Meteor](https://arunoda.typeform.com/to/glm9Qk). 

###Learn more on meteor security 
* [Emily Stark: Meteor Meets Mallory -- Devshop 6 Tech Talk](http://www.youtube.com/watch?v=79uMp-S23MA)
* [Meteor docs](http://docs.meteor.com/#auditargumentchecks)
* [Meteor Security resources](http://security-resources.meteor.com/)