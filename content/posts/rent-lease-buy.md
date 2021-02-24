---
title: "Rent, Lease, or Buy"
date: 2020-12-01
draft: false
image_sources:
  - https://pixabay.com/photos/holiday-priced-hong-kong-for-rent-2770597/
  - https://pixabay.com/photos/contract-signature-lease-available-1464917/
  - https://pixabay.com/illustrations/house-mortgage-home-sold-real-4101306/
tags: [
  opinion,
  refactoring
]
---
# Writing and Refactoring Code
No matter if you are writing fresh new code, or re-writing some old functionality, you need to decide how much effort to put in. 

That may seem like a simple decision to make. Put in as much effort as it takes to meet the requirements. However, in most situations, there are multiple solutions to solve the same problem. One solution may be to hard-code some values in place rather than deciding how they should be set, or shared with the rest of the application. Another solution may be to variablize nearly everything in order to make sure this new functionality may be reused in the future and ensure that all edge-cases are handled properly. 

As I'm sure you can tell, these two example solutions would take a very different amount of time and effort. This is where you need to make the decision on how much effort should be spent on this problem. That decision can be categorized in to one of three ideas. Those are: renting, leasing, and buying. 

Renting is typically a short term commitment. In housing, it could be yearly, monthly, or even weekly. When you enter a lease, it's typically not permanent, but longer term than a rental. In a lot of cases it may be 1 to 5 year commitment. When you buy something, it's more or less permanent. Of course you can re-sell, but that takes considerable more effort than terminating a rental or lease agreement.

# Renting
> A short term commitment where the termination is planned for

{{< figure src="/images/rent-lease-buy/rent-beach.jpg" caption="life's a beach when there's no commitment" alt="for rent sign on beach" >}}

In sofware, there are plenty of times when something "just needs to work". It may be a use-case for a demo, or a bug fix in production. Something that just needs to work long enough to allow for proper planning and thinking through the situation. In these cases, it makes perfect sense to take some "shortcuts". You don't need to follow all the best practices as long as the functionality works as it's expected.

Other times, you may need to add a new feature to an area of the codebase that is planned to be rewritten, or replaced in the near future. Since the entire area will be re-done, you shouldn't spend a lot of time ensuring that your new code follows all the patterns since it's planned to be replaced anyway.

In these cases, the new code you're writing is simply a rental. You're solving a problem, but you know that what you're writing will be changed, or removed in the near future.

For these situations, go ahead and take those shortcuts. Ignore the best practices. Make sure it works, but don't worry if you happen to write a loop that isn't the ideal `O(n)`[^1]

Comments are very useful here. Your future self will thank you. When you're quickly getting something done, it may not always be the most legible. A quick comment to remind yourself, or someone else, of what the intent was will save a lot of confusion later on. It will also help in the upcoming refactoring to know what was _meant to be_. There may be a new class, or library that can do the same thing.

> Pro-tip: Put a date in your comment so it can be known how long it's been there. Especially in a "`This is a rental solution as of Dec 15, 2020, in preparation for the upcoming rewrite`". Later, you can see that the "rental" was actually a "lease", or even a "buy"!

In short, a rental is a quick, sometimes dirty, solution that works long enough for a planned refactoring to happen without as much pressure.

# Leasing
> A longer term commitment, but still temporary. The termination is expected

{{< figure src="/images/rent-lease-buy/lease-contract.jpg" caption="sign up for the long term with a leased solution" alt="person signing contract" >}}

Unlike renting, this situation requires a bit more effort and thought. It doesn't need to be perfect, but you will need to live with it for a while. Possibly even build upon this solution in the near future, until the lease is up and you're able to refactor it into a permanent solution. 

This situation comes up when something needs changed, or added, but the project is due for a major change. Perhaps a license is running out, and management isn't certain they will renew. Another possibility is that the existing code base is being migrated to containers, or microservices.

Both of those situations are known "terminations", where the code may need to change significantly, but the time when that will happen is some time away where you wouldn't be able to give an accurate estimate. 

In these cases, the solution you come up with and code will need to be able to sustain itself for an unknown amount of time, but some shortcuts can still be made in an effort to get things done faster.

Perhaps, there's a plan to write a new validation library, but it's not ready yet. Copy and paste the code that will be in the library in this new solution. (Dont' forget to comment!) It's not ideal to copy paste code around, but this is a lease, it'll probably be fine for a while. When the refactoring time comes, you can simply delete that bit of code.

Another scenario may be separating the code into several classes, or files, or modules. In a lease, just keep everything together as one. This will make minor changes quick and easy. It will also mean you don't need to spend any time or effort on where to place it, what to name it, and so on.

In a lease, you need the solution to be maintainable, but not perfect. One large file, some copied code, and other shortcuts are fine, but it should be more sustainable than a rental since it may be a while before you can go back to refactor it properly.

# Buying
> A long-term commitment. The termination is not expected, but minor adjustments are

{{< figure src="/images/rent-lease-buy/sold-handshake.jpg" caption="seal the deal and buy all in" alt="handshake above sold sign" >}}

"Buying" a software solution means that you plan to use this code in several places, and there are no plans of changing or refactoring.

This is a large commitment, and should involve a lot of effort. It should be planned out, and able to handle a lot of situations and scenarios. In other words, this solution you're buying needs to be robust.

This solution should be maintainable, fully tested, and handle all of the currently known situations as well as some expected edge-cases. Each of those requirements would take some time to implement, but more importantly, they all take a considerable amount of experience to know what is enough and where to spend more time ensuring it's "right". You get that experience from a rented or leased solution. Better yet, one of the earlier solutions with a lot of logging and monitoring in place. This will all help make those big decisions easier with more confidence. 

Starting a new solution, or a refactor of an existing solution, should almost never be considered a buying solution. You don't have the understanding of what works, and what could happen yet. If you don't agree with that statement, and start working toward a maintainable solution that handles a lot of various scenarios, you'll soon find yourself back again to change something that was missed. This miss could be from a forgotten or overlooked requirement, a test case that wasn't considered, or some input value that should have been sanitized before it was passed in.

The other thing that a buy solution allows is documentation. With the additional knowledge of what the solution needs to do from the experience, and the additional time being taken to ensure this solution won't need major changes, the documentation can be solidified. If all the decisions have been made, it may even be possible to have the documentation be written at the same time as the solution. Be sure to write down all of the decisions made so that everyone involved knows what should be happening.

[^1]: Big-O notation is a way to measure code efficiency specifically in loops. [Big O notation](https://en.wikipedia.org/wiki/Big_O_notation)