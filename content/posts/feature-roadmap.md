---
title: "Feature Roadmap"
date: 2021-01-01
draft: false
image_sources:
  - https://pixabay.com/photos/highway-freeway-speedway-road-828985/
tags: [
  opinion,
  refactoring
]
---
# Feature Road (mapping)
This post is not referring to the roadmap you may be used to when speaking within a development team. We're not discussing planning, or future tasks. No, here we are talking about how complete a feature should be. Another way to say it would be: "what is _'done'_"?

In this post, we'll go through a situation where we are working on a site where users can view the most recent news articles from various news outlets. Think about something that would collect all the top articles from CNN, BBC, and other news sites. Almost like the Reddit [r/news](https://reddit.com/r/news) sub-reddit.

> Go back and add options and more features (interstate)
> Finally, add configuration so most situations can be solved (country roads)

# The Plan
I know, I _just said_ "We're not discussing planning". There's always a plan. Even if it's not fully written out, or maybe some things aren't confirmed yet. There is at least _something_ to work toward. This basic plan is generally what gets the stakeholders to agree on spending the time on the feature.

This plan may be just a start of a much larger set of features. Perhaps the "plan" is just "We need to allow people to log in and save a list of favorite news sources." If you let your mind wander with all the possiblities, there is a lot that could enable. There is also a lot of different ways that could be done.

- What should the log in page look like?
- Are users without a profile allowed to access the site?
- How can we protect against people accessing others' profiles?
- Should the user pick a username?
- How strict should the password requirements be?
- Should the password expire?

There are a lot of questions that should be answered. Going back to the initial request, they only need to have a list of sources per user. That's the plan.

# The Interstate
> Get from 'A' to somewhere in the area of 'B'

Think about the roadway system. If you need to get a long distance as quick as possible, you drive on an interstate. There's a high speed limit, there are a lot of lanes in both directions, and there aren't any traffic signals or other things that may slow you down. There are some exit ramps that lead to places of interest. They won't get everyone exactly where they need to be, but they will get almost everyone pretty close to where they are going.

In our situation, we need to build the interstate of getting users to log in and save their list of news sources.

This means we need to solve for the most amount of people to get that feature as soon as possible. In our case, that will likely be using an authentication provider so we won't need to worry about passwords, usernames, security (to a point), and more. For this example, let's use the "Log in with Google" SDK (software development kit).

Of course not everyone has a Google account. Maybe our users don't want to use their Google email address as their username. It also means we won't be able to make a fancy custom log in page, and just rely on the Google site.

For the rest of the feature, we can store the user's Google ID with the list of sources they've added. The details aren't important here. Of course there is still some work to be done to add an "Add" button to the news source, perhaps a page to view all the favorites, and other pieces of this feature. All of that work would need to be done no matter how we got the user to log in.

The goal is to get the most amount of people to using the feature as fast as possible. No, not everyone will be able to have an account. However, a large portion of users will be able to get there quickly.

We've built the feature interstate. Most people can use it to use the account feature, although it's not fully complete. This completes the original request in it's most basic form.

# The Highway
> In this case, there is no "my way", just the highway

In the roadway system, a highway is a wider road with more lanes, higher speed limit, and limited traffic lights. This adds a lot more places to go, and more people can get closer to where they want to be. Driving on the highway between cities means there are more exits on the same road.

In this example, we already have a highway of using a Google account to log in with. Now, we need to get more people to the destination, and closer to where they want to be. Let's add more log in options.

We started this journey with heavy reliance on the Google Authentication process. Now, to be able to allow users who don't have, or don't want to use, Google to sign in to our news listings, we can add additional methods. There are several services available that offer this scenario like [Auth0](https://auth0.com) and [FusionAuth](https://fusionauth.io). For this example, the choice of service doesn't matter. We'll use a different service that allows a lot more options for logging in to our site. This also means, that we will need to change how we're using the user's information. We can no longer rely on the Google Id as the primary identifier. We'll use something available across all the authentication methods like the user's email address. 

Since we are now working with more data, we need to have more logic in our site to manage it all. We're going to need to have a lookup of the user rather than directly using the Google Id provided earlier. We'll also need to adjust the login and account pages to reflect the new options. 

We've now added more complexity to our site and provided the ability for more users to join the site. This means if a person doesn't have a Google account, they may be able to log in with Facebook, Twitter, or others.

We're still relying on other services to tell us about the user. This means that a user would not be able to change their username in our site, or use a different email address. We've built a highway that gets a lot of people pretty close to where they wanted to be. There is still some more work to do to get the people to their house. For that, we'll need to build some country roads.

# Country (Local) Roads
> ...Take me home 

Country, or local, roads usually have one lane in each direction, a lower speed limit, and a lot of traffic lights or stop signs to controll traffic. It's a lot slower, but there are a lot of them and they allow the driver to get directly to where they are going.

Our example site now allows users to sign in with one of many different services, but there are still those users who want to be able to change their username, use a different email address, or not have an account in one of those other services. Let's build out all of those country roads to make sure everyone can get exactly where they want to be.

The highways we built previously could be good enough. Unlike the actual road system, we may not need to build out the country roads. There are a lot of country roads, which means there is a lot of work to do before this stage can be "complete". In this example, those country roads are a custom user login system.

We'll need to do a lot of the same work that the interstate "Google Authentication", and highway "Authentication Service", are doing. The difference in that we are now in full control with all of that complexity built-in.

We'll need to build a custom login page. Store more data about the users, and use custom data to help manage that data. With this, we can now add the ability for any username or email address to be used. We can also add the feature of changing usernames without needing to create another account.

All of this means that there are now a lot of options so that anyone may log in to our site. It also means that there is a lot of complexity. That complexity also means there is a lot of maintenance required. That's partly why country roads are not usually as smooth or flat as the highways and interstates.

# The Road Home
> Home is where you make it

The analogy of feature implementation and road systems is not perfect. A road system needs those country roads so people can drive from thier house to their friends house without leaving the pavement. In feature development, we can stop at building out the Interstate. Sometimes, the cost for implementing more complete features is too high, or not valuable enough. This analogy can help in the planning process to know how much effort should be invested early on. You can start the work and build out an Interstate, then later decide if you need more and should invest in building out a highway or even country roads. You can also skip ahead from building an Interstate to building out those country roads if that's what you decide.

My team has found this analogy easier to discuss than the other common analogy of "t-shirt" sizing. Because the road system can better relate to number of users affected rather than amount of work. Work effort is difficult to estimate, but knowing that you can skip some complexity to allow a majority of users most of what they need means that the work is less difficult (generally speaking).