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
There are a lot of blogs, articles, and even tutorials about how to refactor codebases into a solution that works well in the cloud. This post is not that. This is intended to share a few of the various methods of doing those migrations from an existing, likely large, codebase. It's more than just adding better error handling, retrys, or logging.

There is a lot of other processes, and non-business code that also needs to be upgraded to perform in a cloud environment. Here, we'll go through a process of methodical improvements that help to ease the migration. Rather than performing sweeping changes and ending up in a "death march" of neverending changes and upgrades, we'll instead make smaller changes that can be considered considerable upgrades without doing a lot of work all at once.

The good thing about identifying which changes to make, and when, is that you can stop the migration process inbetween steps in order to continue supporting the application. 

## 

lift-and-shift is an ops-only concern
    move to VMs on the cloud
    ops only concern
lift-and-adjust
    more code changes, but still minor
    utilize more cloud-native features
Containers, cloud-storage, Infrastructure-as-Code
Prepare monolith for strangulation
    isolate sections of code that can run independently and move them to a cloud infrastructure (serverless, vm, static storage...)