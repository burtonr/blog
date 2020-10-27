---
title: "Unit Testing"
date: 2020-10-01
draft: true
---
{{< toc >}}
# Thoughts on Unit Testing
To some surprise, I actually enjoy unit testing the code I write. I didn't used to, I've only recently come into enjoying testing my code. With these three understandings that follow, I actually enjoy writing tests.

Understand this is not an absolute. Depending on the situation, the ideas may change slightly, but overall the concepts remain. 

## Test the Edge
Unit testing is concept of testing a unit of work to ensure it provides the expected result.

Often, that "unit of work" is translated to "method", or "function" within a code base. Meaning, every function should have an accompanying unit test. Starting a new project from nothing as test-driven development, or test-first coding, this works. However, it's not long after starting that new project that there become hundreds of tests. Not a bad thing, but something needs changed. A function needs another parameter, or the object parameter had a property removed or renamed. How many tests have you had to change now? How long did that take? The actual change likely took a fraction of the time to update all the tests.

This idea of a test for every function makes it difficult to make a small change. When updating the tests takes more time than the actual change, developers will often abandon the tests. Either comment out the ones that don't work, delete them, or ignore the failures. 

Having too many tests can actually be worse for the on-going quality of the project than having a couple of thorough tests that are easy to maintain.

To move toward that goal of broad, but thorough, easy to maintain tests, we need to re-define our "unit of work". The work should be what comes to mind when you're discussing the project, or a section of the project. It's not often that the function of making a string lowercase is discussed. However, discussions about creating a new user is. 

In this scenario, the unit tests should be focused around the function `createUser()`. There should not be tests for the `lowercaseUserName()` function. The tests for `createUser()` will have a case for ensuring that the user name is lowercase. That functionality will still be tested, but it will be included in the more important test of ensuring the user is created.

This concept provides three additional benefits. You can quickly identify where a test needs to be added when there's a problem in production. There was an error on new user? Add a test to the `createUser` test section. It allows you to do other things within the `lowercaseUserName()` function without needing to update a bunch of tests. As long as it still provides the proper output, the tests will pass. Additionally, it ensures that the main functionality (`createUser()` in this case) performs the actions necessary. Having a lot of tests for each function may end up not testing the main function that brings them all together. 
> Like rearranging your bedroom. As long as the bed and clothes dresser are still there. That's what's important, not _where_ they are.

In the end, this concept gives you:
- Fewer tests, but higher _quality_ of test
- Developers won't be as cautious to make changes
- Issues can be turned in to tests easier 

## Include Everything
A lot of unit testing tools, and reporting tools, allow the user to define a filter that can exclude certain items from being run or counted in a code coverage report. This feature should be used with a lot of thought and caution. You're providing a safe place to put functionality that will never be tested, and that can be easily abused.

The idea for using the "exclude" or "filter" feature is that there are some things that **cannot** be unit tested. Things like reading from a database, making an API call, and other functionality that is out of our control. The problem is that if that is used, it can be abused. This means developers can put additional logic or functionality inside those files that are ignored. It's easy, and won't cause any immediate problems since there are no tests, and it's being ignored. Tests won't fail, code coverage won't go down, everything is fine until a problem is discovered much later in the development lifecycle hopefully by a QA team, but possibly from a user. 

If we don't exclude anything, we are owning that some things cannot be tested, and that's OK. It's unrealistic to strive for 100% code coverage within a project. Typically, what I've seen, is about 70% coverage goal. If your project has more that 30% of your written code that **cannot** be tested, that's a problem. A problem that can be fixed though. Perhaps the function that makes a call to an external API is actually 100 lines long. You cannot test that function because there is functionality outside of our control in it.

## Code First, Test Later
The idea of Test-Driven Development (TDD) is that the tests are written first. Then, it's a process of having the test fail, update the functionality, the test then passes. The code starts off with a simple implementation to allow the test to pass. This is often done with hard-coded values, or overly simple functions. 

This works, and often works well, in simple implementations, or when the design is very thorough and explicit. More often than not, you will find that this is not the case. Features and functionality is more complex than checking if a string is an anagram. The designs will be vague, and likely change as the features become more complete.

What happens then is the tests that were written first are now broken and no longer relevant. So, those tests are not run, commented out, or deleted entirely. This leads into a similar situation to the first point of "test the edge". When all the tests are broken, nobody wants to take the time to go through and figure out what's broken, why, and how to get it fixed.

A different approach is to "hack"[^1] through an initial implementation without any tests. This initial version may be delivered to a testing team, or possibly as a demo for the client or stakeholder. This allows the actual application to be seen and used by the people who would request changes as fast as possible. There may be some changes requested after this first version is tried out. With the code in a rough state, it's much easier to make those changes, change it faster, and get faster feedback.

Once the test team, stakeholders, or clients are satisfied, at least initially, you now have something to test for. In this case, opposite or test-driven development, we know that it is working the way we want it to rather than knowing how we want it to work. Now, we write the tests to ensure that if anything changes, the outcome will remain the same. 

Again, this lines up with the "test the edge" concept. We're only testing the main functionality to ensure that the results remain unchanged. This is what the test team and clients have agreed to. It also means that we can update the less-than-ideal code to a better state without having to rewrite a bunch of tests. As long as it all produces the same results, we can move things around and make use of some coding best practices.

## Summary
To summarize the ideas above, make it easy to write tests, know what's tested, and don't test too much.

Making it easy to write tests is key to ensuring that new features and changes get covered by tests. If it's even a little bit difficult, tests don't get written. It's difficult to allocate time to the scrum master, manager, or whomever is in charge of making promises.

Knowing what's tested is important to know when there is a problem. If you know about half of the features related to the problem are covered in tests, start looking at the features that are not yet covered. Of course, once you find the source of the problem, be sure to add a test for it!

Don't test too much or you risk making it difficult to keep up with changes. The smaller functions will be covered by a higher level test if it's done right. It will take some experimentation to get it "right", but once it's there, you can achieve a high level over coverage with a minimal set of tests with multiple test cases, or sample data.

[^1]: I use the word "hack" as a way to say the code is written fast and with a focus on making it work rather than best-practices or readability.
