---
title: "A case for paid Open Source"
date: 2021-02-27T12:03:33-08:00
---

![Working in Public: The Making and Maintenance of Open Source Software](/img/oss_book.jpg)*Working in Public: The Making and Maintenance of Open Source Software*


## Making of Open Source software
Reading through Working in Public: The Making and Maintenance of Open Source Software
so much emphasis on the making aspect but not a lot of emphasis on the maintenance aspect, glad this book touches on both

open source developers write and publish their code in public. they enjoy months, maybe years, in the spotlight. but eventually, popularity offers diminishing returns. if the value of maintaining code fails to outpace the rewards, many of these developers quietly retreat to the shadows.

some thoughts on processes in open source, the value it provides, and if and how money should fit into the picture.

### How it's made
"Open source deveolpers were frequently characterized as 'hobby' developers, because the assumption was that only companies could make 'real' software."

Two ways of thinking about how open source software is made
1. Firms

   firms are companies, orgs, any institution with centralized resources
   only companies make software because, from a coordination standpoint, managing the resources required to pull off such a feat would be most efficiently handled within the same organization

2. Commons

   distributed groups of developers that transcended employer affiliations

   commons -> resource that is used, owned, and managed by a community
   rely on self-governed rules

"Commons-based peer production also explains why some developers hold the view that money and open source don't mix. If production runs on intrinsic motivation, money is an extrinsic motivator that is thought to interfere with an already well-coordinated system. Although the commons might not be as profitable as the firm, it's also more resilient, because the currency of its transactions is the desire to participate, rather than money."

## Creation vs Maintenance
"Creation is an intrinsic motivator, maintenance usually requires extrinsic motivation"
-- @balupton, isaacs/github

A project isn't 'done' after the creator pushes out an initial product.

"We're so used to thinking of publication as signifying the end of a responsibility, as when a writer publishes a book, or a pianist finishes a performance. An open source maintainer, on the other hand, is expected to maintain the code they published for as long as people use it"

"This is equivalent of a writer being asked to edit and make changes to the same book every day, into perpetuity, long after they've reaped the initial financial and reputational rewards from its creation. What's more, unlike other content, open source code is relied upon by people, companies, and other institutions that need it to keep working, long after the maintainer's interest has waned. External contributions don't necessarily reduce the burden of maintenance either, because they still require someone to review and merge them"

"The problem is not quite that simple, code is nearly free to distribute, but maintenance can still be expensive. Although it's not immediately visible from the code itself, software does incur a hidden set of costs over time"

## Types of code
### Code as an artifact
static state, could leave it untouched for 50 years and it would still look exactly the same
other people can copy/download the code without costing the author anything
could fork, but in doing so produce a different commodity

"should make no difference to maintainers, from a cost perspective, whether 10 or 10,000 people use it"
two reasons
1. non-rivalry -> my ability to download code doesn't affect your ability to download code  (not exactly true, some marginal costs but will talk more on this later)
2. non-excludability -> if someone has a copy of the code, it is hard to prevent them from sharing that code with others

code in this state is easy to share, copy, and distribute

the purpose of consuming code, in most cases, is not to simply read and study it, but to use it
"open source code derives its value not from its static qualities but from its living ones"
### Code as an organism
when that static code is inserted into their own software, that code comes to life
it might break instantly, it might break their other code, and now they have to rewrite everything around it
when software transitions from static to active state, it starts to incur a set of hidden costs

code that runs in prod is in active state. it's a living organism, like a tree in a forest. it depends on other things, and other things depend on it to survive. hence, a software ecosystem.

## Free as in speech, not free as in beer
the term 'free' referred to what one could do with the software, rather than to its price

but this only accounts for 'static' code
maintenance costs make the difference between "forking as a credible threat" and "forking as a desirable outcome"

free as in puppy
* wow its super fun! it's great!
* as it grows and gets old, geez, theres a lot of time required for me to take care of this thing

code behaves differently in active state
buying a puppy is not like buying furniture, bringing a living creature into one's home signifies the beginning of a new set of responsibilities
### Latent cost of software
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

* creation
  frequently powered by intrinsic motivation -> "hey i wanna build something cool"
  fixed "first-copy" costs
* distribution
  mostly powered by platforms used by creators (e.g. GitHub, GitLab)
  low mostly because of supply-side economies of scale
* maintenance
  typically fall on creators, but not intrinsically motivated
  

## Funding Open Source
as a living organism, other things depend on it
software is like infrastructure, its value is derived from its active dependencies, irrespective of the cost of its construction or maintenance
disconnect between work that is needed vs work that is intrinsically motivated

same question, invest in people or projects

#### Project
funding the project builds institutional memory and makes it easier to manage funds transparently, but funding individuals provides greater flexibility and avoids the centralized governance issues that seem so antithetical to open source

project also tend to attract corporate funding better than individuals do, because companies are more comfortable with paying for code than for talent. in terms of value proposition, projects are attractive to corporate funders because they deliver commensurate benefits: code security and stability, influence, attracting hiring talent

brand affiliation

more concentrated impact, easy to figure out what money is going towards
easier to justify

#### Individual
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