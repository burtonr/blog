---
title: "The Right Solution"
date: 2021-06-09
draft: false
image_sources:
  - https://pixabay.com/photos/highway-freeway-speedway-road-828985/
tags: [
  opinion,
  refactoring
]
---
# Creating the "Right" Solution
The "right" solution is rarely the first solution. That's the post. The right solution is rarely the first solution. Of course, it wouldn't be much of a post if it was just a single sentence. However, once you know that the first solution you come up with will likely not be "right", you can can focus on getting things done.

It's common to overthink a solution to a problem. Especially in software development. There are a lot of design principles and best practices to try and follow. They can also get in the way of solving the problem at hand. When trying to solve a problem, or design a feature, you can quickly fall into the thought process of what you _should_ do.

- "Does this need to be a parameter passed in?"
- "Should I separate this functionality into separate executions?"
- "Does this follow the design principle of least privileged?"
- and so on...

# Make it work
The first step in solving a problem, or designing a new feature is as simple as "make it work". This can be easier said than done when you've been taught, or read a lot, about all the best design patterns.

When you're first getting into solving the problem, it's important to block all those thoughts and desires to make it "right", and focus on getting it done. Put all the logic in one giant function. Make all the calls synchronous. Only use the minimum parameters (if any at all), and hard-code defaults when you need to.

The goal is to have something that solves the problem at hand. The immediate problem, not the perceived problems of testability, scaling, maintainability, or anything else. 

As an example, let's say the problem to solve is that the website you're developing for needs to display the user's name and image when they create a blog post. To solve the immediate problem, we can add a new function to get that information where that function always returns "Scuba Steve" and a picture of a duck.

Obviously, this is not done, but it solves most of the initial problem so that you can move to focus on more specific areas of the problem. With that silly name and picture, you've created an entrypoint to get the data. You've added the execution call to the appropriate place. And, data is being returned. It "works".

# Make it better
Now that the basics are in place, we can focus on making that functionality work better. Rather than always returning the name "Scuba Steve", how would you get the actual user's name? We would need some sort of parameter to be passed in allowing the name to be looked up somewhere. 

If we had started to think about the parameters too early, you may find yourself looking for where to place this entrypoint execution call. You may have been thinking about what data is available at different locations throughout the codebase. You may be thinking about what type the parameter should be. Should it be the username, a user's id, an email address. 

I've been guilty of getting myself lost in those thoughts many times. This is why it's important to start with the "make it work" first. That way, you only need to think about where in the codebase this function needs to be executed. Now that you know where it needs to be, you can think about what you need to make it work better.

The parameters that you'll need may be dependent on where this function is being executed. You may have several options available, or you may be very limited. For this example, let's say the place where we initially executed this new function only has the user's email address available. The data storage for the image doesn't include a field to lookup an image based on an email, only a user's id number. 

We'll add the email address as a parameter to this new function since it's the only thing available. Now, inside that same function, we can make a call to the user's data where the email address is stored so we can look up this specific user's id number. Again, in the same function, take the user's data, and make a call to the data where the image is stored. Now, instead of returning "Scuba Steve" and a duck image, we can return the actual user's name and image.

Of course, that goes against some of the best practices of separating data access calls, doing too much in a single function, and so on, but it is better. Later, we can go back and refactor more to make it "more" better.

# Allow the Solution to be Found
At this point, you've solved the problem and added the new feature of returning a user's name and image. It's not clean code, or testable, or robust, or maintainable, or "good", but it does solve the problem. We could release it to production as-is. Maybe you should.

Once this new function starts being used, you'll have a lot better understanding of what's really needed. Now you can start to add exception handling. Separate the calls to the different data stores. Make the function testable. This is the time to start thinking about the design principles and best practices.

Now that this problem is solved, and maybe even running in a production environment, we can shift our thoughts to how to make it "right". During the process of making the function better by getting actual data, you may have discovered some additional requirements, unexpected execution paths, or other things that weren't apparent when the problem was first brought up. My team calls those "dragons", as in "Careful, there may be dragons down that path." A dragon is just some unexpected problem that comes up that may lead to an entirely different solution. It's important to find those dragons as soon as possible.

Had we started out with thinking about the proper parameters, making sure the new function was testable, and separating all the data access, we may have spent days or weeks before realizing there was some inherit issue with displaying the image at all.

When you ignore the best practices, and solve the problem immediately, sometimes you'll find that the first solution you thought would be best won't work at all and just cause more problems. Solving simple problems one at a time allows the right _solution_ to be found on it's own.

# Don't Panic
Easier said than done. Solve the simple problems first. Then, solve the problems that come up after that. Don't think about the code review, or how someone else will react to seeing "Scuba Steve" in you code. The right solution is out there, but it may be hiding. In a castle. Guarded by dragons. Don't think about picking the lock to the door where the solution is hiding before facing your first dragon.
