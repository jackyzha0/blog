---
title: "A case for funding Open Source"
date: 2021-02-27T12:03:33-08:00
---

## Making of Open Source software
I've just recently made my way through reading *Working in Public: The Making and Maintenance of Open Source Software* by Nadia Eghbal. Not only does it have some absolutely stunning cover art, it touches on a lot of thoughts that have been marinating in my head about the intersection of open source and funding. I've started experiencing the Baader-Meinhof effect and seeing something to do with open source and funding in a disproportionately large number of tweets, conversations, and blogs.

This blog post is an exploration on some of my thoughts on the processes in open source, the value it provides, and if and how money should fit into the picture.

![Working in Public: The Making and Maintenance of Open Source Software](/img/oss_book.jpg)*Working in Public: The Making and Maintenance of Open Source Software*

### How it's made
> "Open source developers were frequently characterized as 'hobby' developers, because the assumption was that only companies could make 'real' software."[^1]

As it stands, there are two main schools of thoughts in thinking about how open source software is currently made.

1. **Firms** are companies, organizations, governments, or any institution with centralized resources. The main argument is that only companies make software because, from a coordination standpoint, the most efficient way to manage the resources to effectively write software is centralized through one organization. Most development done this way is motivated extrinsically.
   
2. **Commons** is a more vague concept that is essentially the spirit of open source. In essence, it's a distributed group of developers that transcend employer affiliations which work on a resource that is used, owned, and governed by its own community. Most development done this way is motivated intrinsically.

Traditionally, software has been seen more as a product of firms: enterprise closed-source software of the likes of Windows, Chrome, Photoshop, etc. More recently, the rise of internet computing and collaboration tools like GitHub have decreased the barrier to entry enough that producing software through a commons is now feasible and very much alive.

Surprisingly, this may also help to explain the why some developers view open source and money as completely separate. If the commons-based method of production is rooted in intrinsic motivation, then money, an extrinsic motivator, will be seen as opposite to core ideals that open source stands for.

## Creation vs Maintenance
> "Creation is an intrinsic motivator, maintenance usually requires extrinsic motivation"
>
> @balupton, isaacs/github [#167](https://github.com/isaacs/github/issues/167)

When an artist finishes a painting, or a runner finishes a marathon, that usually signifies the end of said responsibility. There is no such finish line for an open source project, even after pushing out an initial product.

Creating a project is fun. It's a wild exploration into a new idea, a frivolous journey to create something useful or to learn something new. With the recent rise of cloud platforms, the costs of distributing and sharing a project is almost completely nullified too due to the supply-side economies of scale. Just click a few buttons and your project is now readily available to any of the 4.66 billion people with internet access. For most developers, the process of creation and distribution is intrinsically motivated; it's an enjoyable process.

Maintenance is less so. This is akin to a writer that's been asked to edit, revise, and make changes to the same book day in and day out, long after they've reaped the initial financial and reputational rewards from its creation. Even when the creator wants to drop the project and to work on something else, the pressure of the knowledge that hundreds of thousands of other organizations, companies, and projects rely on that code to keep running keeps the creators tightly shackled to the project. External help doesn't necessarily help either, requiring someone to onboard new contributors and time to review, and merge pull requests.

Code may be nearly free to create and distribute, but maintenance is still expensive.

## Types of code
### Code as an artifact
There are two main ways we can look at code. The first of which is *static* code. Code that, if left untouched for a century, would still look exactly the same. Others can copy and download the code without incurring any additional costs to the author. For the maintainers, it should make no difference in regards to cost whether 10 or 10,000 people use it.

This type of code is a pool resource, it is
1. **Non-rivalry.** My ability to copy the code doesn't affect your ability to copy it. (This isn't exactly true due to some minimal marginal costs but I'll discuss this later)
2. **Non-exludable.** If someone has a copy of the code, it is very difficult to prevent them from sharing that code with others.

Any code that is in this state is easy to share, copy, and distribute. This is the type of code that lives dormant on Github, on StackOverflow answers, and in the GitHub's Arctic Vault[^2]. However, the main purpose of consuming code is not to simply read and study it, but to actually use it.

In doing so, we bring it to life.

### Code as an organism
> "Open source code derives its value not from its static qualities but from its living ones."[^1]

As soon as you hit CTRL-V on that snippet of code, as soon as that static code is inserted into your own, that code comes to life. It might cause a ridiculous amount of red squigglies to show up, break other code that used to be working fine, or force you to rewrite your previous code just to make it work. When code transitions from a resting static state to an active living state, it will start to incur a set of hidden costs.

Like a living organism, it depends on other things and other things depend on it to survive. As a result, this software 'ecosystem' requires constant upkeep to ensure that components don't fall out of balance: dependency bumps, documentation updates, and infrastructure changes.

## Free as in speech, not free as in beer
'Free' software doesn't refer to its price. Infact, 'free' software is often extremely expensive. As Richard Stallman first described free software, it's "free as in speech, not free as in beer." The point Stallman was trying to make was that 'free' refers to what one could do with the software, rather than the price tag.

In reality, code in its alive state is more like a free puppy. In the beginning, it's a great and wonderful thing! Super fun and super cute. As it grows and gets older, you realize "geez, it actually takes a lot of my own time to take care of this thing." Unlike a piece of inanimate furniture, bringing a living creature into one's home comes with bringing in a new set of responsibilities too.

### Latent cost of software
There are two main types of hidden costs in software, one is marginal where costs increase per user, and the other is temporal where costs increase over time.

two subtypes
1. marginal costs
   physical infra -> hosting costs for code (mostly abstracted by third party platforms)
   user support costs -> if you have a billion users, 0.1% require support, 10min per issue, you would need 20,833 support people working 8 hours shifts each day on staff to keep up
   like a traffic jam, everyone wants to drive their own car, but in doing so increases the congestion experiences by others and eventually, themselves
2. temporal costs
   technical debt -> entropy, costs are a function of entropy: the inevitable decay of systems over time
   when code changes, all of the supporting knwoledge that surrounds it must be updated too
   updated Q&A, documentation, tutorials, programming books, videos etc.

   making choices that are easier today but that cost time and money to address later on
   paying this off is almost never intrinsically motivated. it's not the 'fun' part of writing software
   refactoring, managing dependencies, etc.

   a building from 1850s that's had new rooms, plumbing, and electric wiring added piecemeal over the years
  

## Funding Open Source
as a living organism, other things depend on it
software is like infrastructure, its value is derived from its active dependencies, irrespective of the cost of its construction or maintenance
disconnect between work that is needed vs work that is intrinsically motivated

same question, invest in people or projects

### Project
funding the project builds institutional memory and makes it easier to manage funds transparently, but funding individuals provides greater flexibility and avoids the centralized governance issues that seem so antithetical to open source

project also tend to attract corporate funding better than individuals do, because companies are more comfortable with paying for code than for talent. in terms of value proposition, projects are attractive to corporate funders because they deliver commensurate benefits: code security and stability, influence, attracting hiring talent

brand affiliation

more concentrated impact, easy to figure out what money is going towards
easier to justify

### Individual
power of independent creators
from a governance perspective, funding individual developers is better aligned with the distributed nature of open source projects.
e.g. twitch streamers

patronage
often conflated with donations but rather its an interest in following a creator's *future* work based off of their current reputation

its a repeatable thing
a patron is paying for the regular delivery of well-defined value rather than singular one-time value

3 key parts
a) paying -> ongoing commitment to the production of content, not a one-off payment for one piece of content that catches the eye
b) regular delivery -> not random discovery, delievered directly to the user via email or app
c) well-defined value -> what they are paying for and why its worth it

## Mixing money and open source
Q: won't financial rewards adversely affect developer's incentives to contribute
A: yes, but it depends on who you're funding

two major stances
"pay all maintainers!"
"paying maintainers will destroy open source!"

main concensus is that attention is the currency of production
attention in this sense, is then a common pool resource: non-excludable (anyone can bid for their attention) and rivalrous (limited attention)
by charging for access, it then becomes a private good: excludable and rivalrous. this can be done through paid support, patronage, and bounties
by making attention excludable, the quality of contributions will increase as contributors and users compete for the attention of producers

shouldn't fund casual contributors
these people already incur a marginal cost on maintainers -> they need to review and decide whether to merge it or not
also the reason why initiatives like Hacktoberfest don't work (that's a rant for another day)

fund maintainers who already have the proper context to use it effectively

"There is a lot of motivation, both intrinsic and extrinsic, that already powers open source work; we shouldn't disturb the parts that are currently working. Instead, funding can become a useful motivator in places that are absent in any other sort of motivation, such as the later stages of software maintenance."

### Personal Experience
contributing to bentoml
maintenance

[^1]: *Working in Public: The Making and Maintenance of Open Source Software* by [Nadia Eghbal](https://nadiaeghbal.com/)
[^2]: [GitHub's Arctic Vault](https://archiveprogram.github.com/)