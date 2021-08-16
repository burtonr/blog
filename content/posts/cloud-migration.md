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

If your existing logging solution is 

lift-and-adjust
    more code changes, but still minor
    utilize more cloud-native features
Containers, cloud-storage, Infrastructure-as-Code
Prepare monolith for strangulation
    isolate sections of code that can run independently and move them to a cloud infrastructure (serverless, vm, static storage...)