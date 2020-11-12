---
title: "Machines and Intelligence"
date: 2020-11-02T16:17:37-08:00
---

This blog post is adapted from a term paper I wrote for PHIL250: Minds and Machines at UBC. I hope you enjoy the post and learn as much as I did in writing it!

---

# Introduction
Historically, development of AI has taken a very specific approach &mdash; systems that represent the world through symbols and manipulate those tokens in a systematic way to arrive at a result. This type of AI was coined Good Old-Fashioned AI (GOFAI) by John Haugeland (1996). 

This worked well up until around 1984, which was when the field entered an 'AI Winter', a long plateau in progress that was most likely due cynicism in the AI research community that then trickled to media and funding bodies, halting research and development. (Hendler, 2008).

However, with the rise of Moore's Law and the insane amount of compute and data available, a new approach to the development of AI arose &mdash; one that focused on statistical methods and connectionist networks like artificial neural networks (Hendler, 2008). Haugeland (1996) dubbed this approach to AI design New Fangled AI (NFAI).

This paper will examine factors that differentiate GOFAI and NFAI systems, such as their ability to adapt to changes in input, and the explainability of their outputs and internal representations. It will also examine current work in integrating the two approaches to Artificial Intelligence to make an artificial general intelligence.

# GOFAI Systems
Since the inception of the term GOFAI, the basic idea still remains unchanged: thinking as internal symbol manipulation. Within these GOFAI systems, symbols are representative of aspects of our world. These symbols are manipulated in a systematic and logical matter, performing a series of deterministic steps that results in another sequence of symbols (Haugeland, 1996).

A very common example of GOFAI are AI systems called expert systems, which are computer systems that emulate the decision making ability of a human expert (Jackson, 1998). They solve problems via decision-tree reasoning, figuring out whether to perform certain actions based off of if-then rules.

However, just being able to solve a problem shouldn't be sufficient for intelligence. So what qualifies it? At its core, GOFAI can be considered 'artificially intelligent' because of semantic interpretation. If those symbols represent aspects of our world, the result, which is also a symbol sequence, they can be *translated* back into aspects of our world. This is called semantic interpretation, which "seeks to construe a body of symbols so that what they mean ('say') turns out to be consistently reasonable and sensible, given the situation" (Haugeland, 1996). 

# NFAI Systems
NFAI, on the other hand, is a diverse and still rapidly evolving set of systems and algorithms. It is more of a grab-bag term, roughly meaning any sort of scientific mind design that is not GOFAI (Haugeland, 1996). Under this umbrella are connectionist networks, which are networks composed of lots of simple units that are interconnected with various strengths. This paper will mostly focus on connectionism as a synecdoche for the greater umbrella of NFAI.

Some classic examples of connectionist networks include convolutional neural networks (CNNs), which are a form of image classifiers (Buckner, 2019). These networks operate by applying filters or kernels to an input between layers of the network. Each of those filters have their own set of strengths that will learn and evolve over time to identify certain 'features' from the input. Similar to cell assemblies in animal perceptual systems, these filters assemble more complex patterns using smaller and simpler patterns (Zhang et al., 2018).

These connectionist networks are very inspired by the structure of the brain, with its hierarchical patterns and compositional nature (Churchland, 1990), rather than rational manipulation of symbols that is observed in GOFAI.

# The Potemkin Village Analogy
While it is obvious that GOFAI and NFAI are very different approaches to constructing AI systems, how do they differ in their resilience to failure? An analogy that may be useful in visualizing this is a potemkin village &mdash; a fake village that is built to resemble and deceive others into thinking it is real. Similarly, AI systems attempt to build a sort of 'potemkin village' that "works well on naturally occurring data, but is exposed as fake when one visits points in space that do not have high probability" (Goodfellow et al., 2014).

GOFAI systems are excellent at "processing syntactical patterns like those characteristic of logical formulae, ordinary sentences, and many inferences" (Haugeland, 1996), but are also very narrow-minded and vulnerable when it comes to unexpected variations or oddities in the input given. The potemkin village that a GOFAI system may construct will hold up if only seen from the intended angles, but any slight deviation from an intended or expected input would shatter the illusion immediately.

NFAI systems, on the other hand, are "adept at finding various sort of similarities among patterns, at recognizing repeated (or almost repeated) patterns and filling in missing parts of incomplete patterns" (Haugeland, 1996). These also happen to be the exact things that GOFAI systems struggle with. The potemkin village that a NFAI system may construct will hold up much more robustly to unexpected patterns or noisy input, but will, at heart, still be a fake village.

# Rationality and explainability
In GOFAI systems, intentionality &mdash; the meaning and semantics behind the tokens &mdash; is injected through explicit programming by those who create it. These GOFAI systems are able to process these tokens and make conclusions based off of logic and reason rather than just trial-and-error. Case in point, expert systems. These if-then statements can easily explain decisions by showing which parts evaluated as true or false in its decision making process (Jackson, 1998). 

Connectionist systems, for the most part, are very hard to explain and are often dubbed black-box models due to the hidden nature of its internal workings. Unlike GOFAI systems, its internal representation model is defined by the state of the entire network rather than that of any single unit &mdash; this is commonly referred to as a distributed model of connectionist representation (Crane, 2003) and is often claimed to be one of the distinctive features of connectionism.

# Models of representation
To put it in sound terminology, note that in the GOFAI system, the *tokens* are the objects of formal processing here; the system itself is the vehicle of computation. The tokens themselves are also *representations* of aspects of the world, so they are vehicles of mental content. In GOFAI systems, tokens are both the vehicle of computation and the vehicle of mental content.

This is in contrast with connectionist systems where computation is performed at the level of simple units (unit activations, backpropagation), meaning the units are the vehicles of computation. However, as these systems use a distributed model of representation, it is not a single unit that 'represents' something, but rather the "network state as a whole thats interpreted as representing" (Crane, 2003). Thus, in connectionist systems, the vehicles of computation (units) need to be the vehicles of representation (network state).

# Integrating GOFAI and NFAI
Given that GOFAI and NFAI systems seem so vastly different in their strengths, how might one go about reconciling them?

One approach is to combine both into one system. These are used when there’s a rational, known, and algorithmic way to process a subproblem. Systems like AlphaZero, a connectionist based Go playing system, use mixed systems to achieve the level of performance they report. Although at heart, AlphaZero uses a deep neural network to assess new positions, it also uses a Monte Carlo Tree Search (a GOFAI algorithm) to determine its next move based of the assessment of the neural net (Silver et al., 2017).

Another, less researched method, is interpretable connectionist systems. As traditional connectionist networks rely on the network state being the vehicle of representation, the complexity, depth, and scale of modern connectionist models means that it is becoming increasingly difficult for humans to interpret the output. The field of explainable AI (XAI) focuses on incentivizing connectionist networks to develop localist representations (i.e. moving away from having the vehicle of representation be at the network level, but at the unit level). Zhang, Wu, and Zhu of UCLA recently showed that it is possible to train a CNN to use 'interpretable filters', which encourage networks to group feature detectors into single filters, showing the possibility of moving from distributed representations to more local representations.

# What is AGI?
While intelligence can be understood in many ways, this paper will focus on examining the prospects of emulating or achieving the capacity to understand or learn anything a human can &mdash; the hallmark of an artificial general intelligence (AGI).

Most commentators would agree that current AI systems fall short of implementing general intelligence (Buckner, 2019). These are narrow AI systems, which are used to accomplish or solve specific tasks like the game of Go or language translation, rather than to attempt to create a system capable of AGI. So, what's stopping us from making the transition from domain-specific algorithms to domain-general algorithms?

# How close are we to AGI?
None of the current GOFAI or NFAI approaches are general problem solvers by any means. Our best efforts to do so are at best like that of AlphaZero: a semi-general algorithm that can 'generalize' to a small handful of problems like chess, checkers, and go, yet fail to solve anything other than board games (Silver et al., 2017).

One problem that stumped earlier attempts at AGI was the 'common-sense problem': how do we represent 'common-sense' information that is obvious to most humans in a way that is accessible to AI systems that use natural language? Unsurprisingly, this problem of storing all of this information was solved by the massive explosion in compute and data in the past few decades (Hendler, 2018).

However, the difficult part of this problem, choosing what subset of that huge information bank is relevant in any situation, remains a huge unsolved problem. How do we update our database of knowledge when relationships between symbols change? This is often called the frame problem.

# Dissolving the frame problem
Dreyfus (2008) posits that any AI systems which attempt to tackle the frame problem through storing relevant frames are bound to failure. He argues that, "human beings do not simply store common-sense information," rather they "directly perceive and act upon significance in their environment". In his view, a more Heideggerian approach to AI will dissolve this problem.

# Heideggerian AI
Heideggerian AI, in its most basic sense, is concerned with 
the concept of Dasein, which literally means 'Being-there' (Solomon, 1972). Through the use of this expression, Heidegger calls to attention the fact that a human cannot exist or be taken into account without being existent in context of a world with other things &mdash; "to be human is to be fixed, embedded, and immersed in the physical, literal, tangible day to day world" (Steiner, 1978).

Dreyfus believed that, for any AI system to achieve any sort of general intelligence, it must also exhibit Dasein. Thus, "a successful Heideggerian AI would need a perfect model of the human body – and by implication, that Dasein must be expressed as a human being, organically as well as existentially" (Dreyfus, 2008).

# A non-humanistic approach
However, Steed refutes Dreyfus' overly humanistic interpretation of Heideggerian AI, believing that a AI model only needs to be "embedded and embodied such that what AI experiences is significant for AI in the particular way that AI is," intelligence would be possible by Heideggerian standards (Steed, 2019).

The refutation against a purely anthropocentric view of AI brings to light an important concept: the multiple realization argument. Emulating or copying human intelligence isn't the only way to achieve intelligence that rivals that of humans.

Contemporary AI systems are almost always used as a problem solving tool, a means to tackle uniquely human problems and to convey results that are semantically useful to us. As a result, these approaches are doomed to be constrained by human problems. 

However, by looking outside the anthropocentric view of intelligence, it may not share these human problems with us and "perhaps an authentic, free AI system does not converge to a solution that is interpretable from a human standpoint at all" (Steed, 2019). 

AI is already capable of learning, adaptation, and basic Being-in-the-world. Thus, to achieve general intelligence, we should allow AI to contemplate its own problems and existence.

# Bibliography
- Buckner, C. (2019). *Deep learning: A philosophical introduction.* Philosophy Compass, 14(10), e12625.
- Churchland, P. (1990). *Thinking: An invitation to cognitive science.* Vol. 3., pp. 199-228.
- Crane, Tim. (2003). *The Mechanical Mind.* doi:10.4324/9780203426319. 
- Dreyfus, Hubert L. (2008) *Why Heideggerian AI Failed and How Fixing It Would Require Making It More Heideggerian.* The Mechanical Mind in History, pp. 331–362., doi:10.7551/mitpress/9780262083775.003.0014. 
- Goodfellow, I., Shlens, J., & Szegedy, C. (2014) *Explaining and harnessing adversarial examples.* ArXiv Preprint ArXiv: 1412.6572.
- Hendler, J. (2008). *Avoiding another AI winter.* IEEE Intelligent Systems, (2), pp. 2-4.
- Huageland, John. (1996). *What Is Mind Design?* Mind Design II, doi:10.7551/mitpress/4626.003.0001. 
- Jackson, Peter (1998). *Introduction To Expert Systems* (3 ed.). Addison Wesley. p. 2. ISBN 978-0-201-87686-4.
- Silver, D., Hubert, T., Schrittwieser, J., Antonoglou, I., Lai, M., Guez, A., ... & Lillicrap, T. (2017). *Mastering chess and shogi by self-play with a general reinforcement learning algorithm.* arXiv preprint arXiv:1712.01815.
- Steed, R. (2019). *AI is Heideggerian Enough, But Can It Be Authentic?* Unpublished manuscript, Carnegie Mellon.
- Steiner, G. (1978), *Heidegger*, The Harvester Press Limited, Sussex
- Solomon, R. (1972), *From Rationalism to Existentialism: The Existentialists and Their Nineteenth Century Backgrounds*, Harper & Row, New York.
- Zhang, Q., Nian Wu, Y., & Zhu, S. C. (2018). *Interpretable convolutional neural networks.* In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (pp. 8827-8836).