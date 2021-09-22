---
title: "Cloud Migration"
date: 2021-07-01
draft: true
image_sources:
  - https://pixabay.com/photos/highway-freeway-speedway-road-828985/
tags: [
  opinion,
  refactoring,
  cloud
]
---
# Migrating to the Cloud
There are a lot of blogs, articles, and even tutorials about how to refactor codebases into a solution that works well in the cloud. This post is not that. This is intended to share a few of the various methods of doing those migrations from an existing, likely large, codebase. It's more than just adding better error handling, retrys, and logging.

There are a lot of other processes, and non-business code that also needs to be upgraded to perform well in a cloud environment. Here, we'll go through a process of methodical improvements that help to ease the migration. Rather than performing sweeping changes and ending up in a "death march" of neverending changes and upgrades, we'll instead make smaller changes that can be considered considerable upgrades without doing a lot of work all at once.

The good thing about identifying which changes to make, and when, is that you can stop the migration process inbetween steps in order to continue supporting the application with bug fixes, new features, and other maintenance. 

## Lift and shift
The "lift and shift" approach is one way to dive head-first into a cloud environment. This is where you would create a Virtual Machine in your cloud provider, and move all your existing code onto that VM. 

This change requires little, if any, application code changes. You would still be running in a familiar host, and likely a lot of the tooling will still function as-is.

That is the "lift" portion. The "shift" portion involves more of the operations process. With the move to a cloud VM, the deployment process would need to be updated to point to the new destination. There is also the work involved in securing the VM now that it is no longer within your local network. There are plenty of ways to solve this problem, but the main point is that this change shouldn't affect the application directly, requiring the code to change, at least initially. 

Simply doing this one step, you could tell management that you're now "in the cloud". Done! 

This is of course only a part of the process. There are still a lot of changes to be made in order to take advantage of being in a cloud environment, but those things can be added later on. What this does do, is gets everyone thinking about the cloud more than just on a whiteboard. Lifting and shifting means that you will now be getting billed for resources used. You will also have to consider different security and access concerns. Granted, these are not major changes, but it does make the cloud environment a more prominent discussion point across several different teams in the organization.

This is a good move to make if you're having trouble getting authorization to make the move into a cloud environment. From here, the changes will be easier to make since the ideas will be easier to explain with everyone on the same page about what it means to be in the cloud. You may be surprised at how quickly non-developers' understanding of the cloud becomes once it is a part of the business operation.

## Lift and Adjust
An alternative approach is to make some minor adjustments to the application code during the lift and shift process. This would involve changing some parts of the application that may be easier to understand, faster to implement, and take advantage of some of the cloud features. 

Some things that may be good first processes to make those changes could be logging, messaging, and authentication. Each of these items are provided by all the major cloud providers as a service and also work well with existing implementations with minor changes.

If your existing logging solution is writing to a log file on the host server, you could quickly change that to either write to `STDOUT`, or use the SDK provided by the cloud provider. Likely, the logic that writes to the existing solution is a shared, and isolated bit of code. This upgrade would be focused on that one small section, and wouldn't require a large sweeping change. It can also easily be tested and verified. 

Upgrading your logging solution is a big gain with minimal effort. All the major cloud providers offer a service for logging that includes some level of search and metrics built in. Being able to utilize that early on, and throughout the remaining tasks of migration will be very helpful for everyone.

Messaging, and Authentication are two other areas that are likely already isolated in the current solution. They are also provided as a service in all the major cloud providers. Upgrading these features to be cloud-native can add a great deal of benefit with the additional features provided.

### Something to be aware of
As you're migrating some of these features into cloud services, the costs will increase immediately. Logging, messaging, and authentication are all billed on a per-access plan. This means that each time you read or write to one of those services, a charge is added. Most of the time, there is a generous amount before a charge is incurred (1 million log writes before billing as an example). These features are typically accessed a lot. It may be that in the current solution, there is a log message on every function call by default. This could quickly run into a chargable amount of log entries, and thus start adding up the charge on the monthly bill.

Be sure that the management teams are aware that there will be an immediate cost. It may seem like a lot of money initially for something as small and simple as log messages.

It helps to consider the cost is more than just storing log messages. It provides general access to those logs so that it's easier for everyone to see what's happening. The cost also includes searching, and metrics gathering. Things that may not have been available in the current solution writing to a local file.

With those additional perks included, the price is much more reasonable. Also, you may be able to go through and adjust the logging, or messaging, to be less verbose. Writing less logs, with more meaning, will help with the cost, and also may help with understanding as well.


## Container-ization, Storage, and DevOps

Containers, cloud-storage, Infrastructure-as-Code
Prepare monolith for strangulation
    isolate sections of code that can run independently and move them to a cloud infrastructure (serverless, vm, static storage...)