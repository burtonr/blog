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
There are a lot of blogs, articles, and even tutorials about how to refactor a codebase into a solution that works well in the cloud. This post is not that. This is intended to share a few of the various methods of doing those migrations from an existing, likely large, codebase. It's more than just adding better error handling, retries, and logging.

There are a lot of other processes, and non-business code that also needs to be upgraded to perform well in a cloud environment. Here, we'll go through a process of methodical improvements that help to ease the migration. Rather than performing sweeping changes and ending up in a "death march" of never ending changes and upgrades, we'll instead make smaller changes that can be considered considerable upgrades without doing a lot of work all at once.

The good thing about identifying which changes to make, and when, is that you can stop the migration process in-between steps in order to continue supporting the application with bug fixes, new features, and other maintenance. 

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
As you're migrating some of these features into cloud services, the costs will increase immediately. Logging, messaging, and authentication are all billed on a per-access plan. This means that each time you read or write to one of those services, a charge is added. Most of the time, there is a generous amount before a charge is incurred (1 million log writes before billing as an example). These features are typically accessed a lot. It may be that in the current solution, there is a log message on every function call by default. This could quickly run into a chargeable amount of log entries, and thus start adding up the charge on the monthly bill.

Be sure that the management teams are aware that there will be an immediate cost. It may seem like a lot of money initially for something as small and simple as log messages.

It helps to consider the cost is more than just storing log messages. It provides general access to those logs so that it's easier for everyone to see what's happening. The cost also includes searching, and metrics gathering. Things that may not have been available in the current solution writing to a local file.

With those additional perks included, the price is much more reasonable. Also, you may be able to go through and adjust the logging, or messaging, to be less verbose. Writing less logs, with more meaning, will help with the cost, and also may help with understanding as well.


## Container-ization, Storage, and DevOps
The beginning of the end, or the end of the beginning. Now that the application is set up to start using some of the cloud features, specifically logging, you can start to migrate to a fully cloud-native application. 

In my opinion, there are three core pieces of a cloud-native application. Containers, Storage, and Infrastructure-as-Code (IaC). There are a lot of other considerations. Some others are detailed in the [12-factor app](https://12factor.net/) which describes how to make an application declarative, deployable, and scalable. More things to consider include networking, health checks, and self-healing. Look for a future post with more details about cloud-native applications.

For now, at the end of the beginning of your cloud migration process, focus on the three parts I outlined earlier.

### Containerization
Containers are the core of cloud technology. Containers allow for reproducible environments, portability, and ease of deployments. Applications running in a container can quickly and easily be deployed and upgraded. Additionally, making an application run in a container can be straight-forward. At the root of a container, it's just a minified operating system with Linux, Windows, or a variety of other Unix-based operating systems.

It's possible no code changes will need to happen to get your application to run inside a container. Although, most likely, it will require some minor changes depending on what the application does, or communicates with. Add a Dockerfile to your code base and get started trying it out to see what needs to be adjusted, if anything at all. There are sample Dockerfiles for any language your application is written in. Start with the sample, and add things that your application needs. Once it's up and running as a container, it will be much easier to go back and adjust the container image to be smaller, or more performant. 

Every cloud provider offers a Containers-as-a-service offering where you can provide minimal configuration to have a single container running in the cloud. If you've updated your application to use cloud logging as mentioned in the lift-and-adjust section, you'll still be able to keep an eye on any problems that may come up.

With the application running in a container, new team members can get started faster, deployments can be simplified to pushing the image, and updating the configuration.

### Storage
When running your application in the cloud, or in a container, keep the idea in mind that there is no local disk. The storage system in both are ephemeral and will disappear if your application stops or crashes. Cloud Storage is the way to compensate for that 'feature'.

TODO!!! 

### Infrastructure-as-Code (IaC)
Infrastructure-as-Code is the idea that all of the infrastructure is defined in a text (code) file to allow for quickly reproducing, or duplicating entire environments in the cloud.

This concept is an important step in the migration to the cloud. Where you don't have complete control over the servers your code is running on. Additionally, most services including server compute time, is calculated per minute. The ability to destroy everything when you aren't using it can save a lot of money in a short amount of time. Finally, being able to set up an _exact_ duplicate of your production environment for testing, bug reproduction, or upgrade validation is invaluable when your application is depended on by others.

There are many options for managing your infrastructure as a code repository. These options range from a single shell script, to a complete product offering with it's own independent management. As you're just beginning the migration into the cloud, I would recommend avoiding the tools and product offerings. These are very nice, and have a lot of great features, but will distract from the main goal of having repeatable, coded infrastructure. Start off with a couple shell scripts that simply execute commands from your cloud provider's CLI. Google Cloud (`gcloud`), Azure (`az`), AWS (`aws`), and others have a downloadable CLI tool that can operate on most of the offered services. 

Start with a script that can create a container instance, and deploy an image. Although it may not be a replication of production, it will provided you and your team the ability to quickly and repeatably deploy a container into the cloud to test with. Make small steps like this working your way toward a production, or at least test, grade environment. Ensure everyone who can use it does. This will ensure that any mistakes get fixed, and new features get added.

Around the time you're nearing a production-like environment in shell scripts, you'll be wishing there was an easier way. There is! This is now the time to begin looking at the available tools. Terraform, Ansible, Salt, Chef, and more. There are a lot of options, and knowing which one to choose is easier now that you have something working for you. With the shell scripts you started with, you now know what features to look for and how you want to manage the code. 

Choosing a tool is a big commitment. The choice will determine what's possible with your infrastructure, or more importantly, what's not possible. Infrastructure code is notoriously difficult to test. This means that changing to a different tool is a time consuming process that takes a lot of great care to ensure everything still works after the switch. Most tools use their own custom language or syntax, making it more difficult to swap tools at a later time. It's not impossible, but it is a significant amount of work. All that to say, choose wisely and ask questions to the respective communities.

Once the tooling is in place, changes will be easier to manage. Adding additional resources, or creating temporary environments, and even creating complete blue/green environments in production will be easy and smooth! Ok, maybe not quite that easy, but it can be! Don't let the infrastructure code base slip out of relevance. It's easy to forget about it after some time of using it. Push everyone who can to use the infrastructure code to ensure it stays relevant. Discourage manual changes to the environments. It may be the case that a developer needs something in a test environment and discovers the button to enable it on the cloud provider's site. They may then consider "just pushing the button each time" when they create a new environment. Then they recommend the new person to do the same because it's easy. After some time of that happening, the infrastructure code becomes only a small step in the process of setting up a new environment rather than the **only** step.
 

Prepare monolith for strangulation
    isolate sections of code that can run independently and move them to a cloud infrastructure (serverless, vm, static storage...)