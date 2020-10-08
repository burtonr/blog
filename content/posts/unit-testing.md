---
title: "Unit Testing"
date: 2020-10-06
draft: true
---
# Thoughts on Unit Testing
To some surprise, I actually enjoy unit testing the code I write. I didn't used to, I've only recently come into enjoying testing my code. With these three understandings that follow, I actually enjoy writing tests.

Understand this is not an absolute. Depending on the situation, the ideas may change slightly, but overall the concepts remain. 

## Test the Edge
Unit testing is concept of testing a unit of work to ensure it provides the expected result.

Often, that "unit of work" is translated to "method", or "function" within a code base. Meaning, every function should have an accompying unit test. Starting a new project from nothing as test-driven development, or test-first coding, this works. However, it's not long after starting that new project that there become hundreds of tests. Not a bad thing, but something needs changed. A function needs another parameter, or the object parameter had a property removed or renamed. How many tests have you had to change now? How long did that take? The actual change likely took a fraction of the time to update all the tests.

This idea of a test for every function makes it difficult to make a small change. When updating the tests takes more time than the actual change, developers will often abandon the tests. Either comment out the ones that don't work, delete them, or ignore the failures. 

Having too many tests can actually be worse for the on-going quality of the project than having a couple of thorough tests that are easy to maintain.

To move toward that goal of broad, but thorough, easy to maintain tests, we need to re-define our "unit of work". The work should be what comes to mind when you're discussing the project, or a section of the project. It's not often that the function of making a string lowercase is discussed. However, discussions about creating a new user is. 

In this scenario, the unit tests should be focused around the function `createUser()`. There should not be tests for the `lowercaseUserName()` function. The tests for `createUser()` will have a case for ensuring that the user name is lowercase. That functionality will still be tested, but it will be included in the more important test of ensuring the user is created.

This concept provides three additional benefits. You can quickly identify where a test needs to be added when there's a problem in production. There was an error on new user? Add a test to the `createUser` test section. It allows you to do other things within the `lowercaseUserName()` function without needing to update a bunch of tests. As long as it still provides the proper output, the tests will pass. Additionaly, it ensures that the main functionality (`createUser()` in this case) performs the actions necissary. Having a lot of tests for each function may end up not testing the main function that brings them all together. 
> can't see the forest for the trees

In the end, this concept gives you:
- Fewer tests, but higher _quality_ of test
- Developers won't be as cautious to make changes
- Issues can be turned in to tests easier 

## Include Everything
A lot of unit testing tools, and reporting tools, allow the user to define a filter that can exclude certain items from being run or counted in a code coverage report. This feature should be used with a lot of thought and caution. Another way to think of this is putting a {{??????: curtain over a room???}}. You're providing a safe place to put functionality that will never be tested.

The idea for using the "exlude" or "filter" feature is that there are some things that **cannot** be unit tested. Things like reading from a database, making an API call, and other functionality that is out of our control. The problem is that if that is used, it can be abused. This means developers can put additional logic or functionality inside those files that are ignored. It's easy, and won't cause any immediate problems since there are no tests, and it's being ignored. Tests won't fail, code coverage won't go down, everything is fine until a problem is discovered much later in the development lifecycle hopefully by a QA team, but possibly from a user. 

If we don't exclude anything, we are owning that some things cannot be tested, and that's OK. It's unrealistic to strive for 100% code coverage within a project. Typically, what I've seen, is about 70% coverage goal. If your project has more that 30% of your written code that **cannot** be tested, that's a problem. A problem that can be fixed though. Perhaps the function that makes a call to an external API is actually 100 lines long. You cannot test that function because there is functionality outside of our control in it.

## Code First, Test Later