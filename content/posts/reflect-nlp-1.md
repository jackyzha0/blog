---
title: "reflect: NLP model explained pt. 1"
date: 2020-05-10T08:51:56-07:00
---

![An image of the reflect block page](https://miro.medium.com/max/1400/1*yjCs2Mmcve8wNI1pdfXelw.png)*How do we tell that this is a “valid” intent?*

A (not so) brief exploration of how we tackle classifying intents in reflect. Part 1 will touch on defining the problem we’re trying to solve, the data we have, and how we pre-processed it. Part 2 will focus on the architecture of the model we built, how well it does, and thoughts on improving it for the future.

## The problem

Classifying intents is at the core of reflect. When a user inputs an intent, its reflect’s job to figure out whether that intent should let them into the website.

> How do we make sure “do some marketing work for reflect” is classified as productive but “watch cute dog videos” isn’t?

## Why it’s so difficult

A lot of it comes down to the fact that natural language processing (NLP) is a very difficult task. What does the sentence “learn about physics” mean, and how is it semantically different from “asdflkj I can’t do work”?

We can’t just parse for keywords and just allow a user in if we see the word “work” because that word can mean different things in different contexts. For example, “I’m not doing any work right now” would have otherwise been classified as valid. Thus, we can employ the help of a machine learning algorithm to help us capture this deeper meaning.

Specifically, the form of machine learning we will be using is called **supervised learning, **in which we give an algorithm a bunch of labelled data, tell it what it’s doing wrong, and let it ‘learn.’ Through doing this, hopefully the algorithm will be able to generalize and make predictions on unseen data too.

## The data

Of course, if we want to perform supervised learning, we’re going to need a lot of data. Where are we going to get all of it? Luckily, we were able to get it through 3 different sources.

### Survey data (444 entries)

Our team sent out an interest survey in early January in which we asked 3 questions:

1. How would you answer if you were trying to visit a distracting site while trying to focus? (eg. youtube, facebook, etc)

1. How would you answer if you were trying to visit a distracting site to take a quick break from your work? (eg. youtube, facebook, etc)

1. How would you answer if you were trying to visit a distracting site like Facebook but to do work? (e.g. make a marketing post)

We used these answers to form the basis of our very first dataset. We ended up getting a surprising amount of entries, ending with 148 responses to 3 questions and totalling 444 different observations. Here’s what some of that data looks like after tidying it up:

> We classified any answer to Q1 as invalid and Q2 + Q3 as valid


| intent | valid |
|-|-|
| I am watching a 5 minute video to take my mind off not being productive :/ | no |
| I'm just bored | no |
| I’m bored/tired and trying to relax | no |
| ... | ... |
| work is pretty boring, i need to take a quick break I just can't focus atm | yes |
| I finished all my work for today so I'm going to take a break now! | yes |
| getting some advertising done for my club | yes |
| I need to make a post on Twitter for my job announcing the latest update to our site | yes |
| I'm trying to network | yes |
| ... | ... |


### Closed Beta (790 entries)

After we made a basic dataset, we were able to make our first (admittedly not great) model. But in doing so, this let us create an MVP to which we could use to actually test with. We then deployed this model for use to our closed beta testers and collected their responses (with consent of course!) along with the website it was input on. This was then converted into a .csv file. A few examples are show below:

| intent | url |
|-|-|
| to do some marketing | facebook.com/ |
| i cannot focus on my work | instagram.com/ |
| fuel my crippling social media addiction | facebook.com/ |
| ... | ... |

These were then hand-labelled by our reflect team in a similar format as the survey data we collected earlier.

| intent | valid |
|-|-|
| to do some marketing | yes |
| i cannot focus on my work | no |
| fuel my crippling social media addiction | no |
| ... | ... |

### Closed Beta Corrections (37 entries)

Finally, we created a Google Forms through which we directly asked beta testers if a decision made by reflect’s intent classifier was faulty. Specifically, we asked what they input, and what they expected. Here are a few examples:


| input | valid |
|-|-|
| reply to a friend about a lab | yes |
| listening to a youtube music playlist | yes |
| goof off as much as possible | yes |
|...|...|


This entire section of the dataset was only 37 observations, but it drastically helped us reduce false positives and false negatives by focusing specifically on misclassifications.

After aggregating and combing all our data into one common format, we ended up with a grand total of 1271 observations. They looked something like this:


| input | expected |
|-|-|
| fail school by watching youtube | no |
| sdlkjasd | no |
| making a quick product post (should take <10 min) | yes |
| ... | ... |


### So?

Now that we have the data, can we just throw it into a machine learning model? Unfortunately, the answer is no, not quite yet.

## Data augmentation

Our dataset is still pretty small, even after aggregating all of our data. It most definitely doesn’t cover all of our bases for all the possible things that future users could possibly input. So, how can we “upsample” our data to get more of it? Well, it turns out that the field of Natural Language Processing has quite a few tricks to augment our data.

### Sentence Variation

Essentially what sentence variation is, is just replacing a few words of given sentences with their synonyms. If we have a sentence like “I’m trying to make a marketing post,” we can swap out singular words with their synonyms and tell our network that it means the same thing.

In this example, we could get something like “I’m attempting to fabricate a marketing post”. Adding these additional sentence variations will allow our machine learning model to learn semantic relationships between similar words (e.g. fabricate and make have similar meaning)

### Sentence Negation

Additionally, if we add a ‘not’ in the sentence, it should flip the meaning of the sentence. An example would be “learning about physics” is valid, whereas “not learning about physics” is not. However, if the sentence already contains ‘not’ (e.g. “I’m not being productive”), adding another ‘not’ would make the sentence too complex and obfuscated, so we just label it as invalid. In essence, we just add ‘not’ to a bunch of sentences and label them as invalid. This helps us to combat intents which use negations in a sort of round-a-bout way to confuse the algorithm.

### Shuffled Sentences

If we take an existing, valid sentence and completely shuffle the words, the resulting sentence should be invalid. An example would be “to watch a crash course video*” should be valid whereas “video course a watch crash to*” should be invalid. Basically, we’re just shuffling existing sentences and also labelling them as invalid. This helps us to combat intents which grammatically make no sense, but are otherwise valid.

### Garbage Sentences

We can also take completely random words from the English language and put them together. The resulting sentences should all be invalid. For example, “*untinkered phalangitis shaly quinovic dish spadiciflorous unshaved” *clearly makes no sense. However, the addition of these gibberish sentences allows our model to be more robust against foreign words and out-of-vocabulary terms.

### Vocabulary-mix Sentences

Last but definitely not least, we can take the most common words in our dataset and mash them together. This should yield us a bunch of sentences which contain “key words” but should be marked as invalid because the context in which they are used makes no sense. For example, “video look watching” and “get research facebook take need want need message watch” are both clearly gibberish sentences, but they have a lot of keywords that one would think would let you in (e.g. video, research, watching, etc.). This lets us be more robust against those who try to get around the algorithm using keywords.

## Data preprocessing

What about now? Can we throw it into the neural network yet? Well, no. We may have increased the amount of data we have to work with, but we also need to convert it to a form that is easy to understand for both the computer and for our algorithm. We do that with a series of functions that we apply on our data.

### Strip punctuation

As the name suggests, we remove all punctuation from the input phrase. We found that including the punctuation hurt our performance, most likely due to the fact that they offer very little in terms of semantic meaning and obfuscate the real meaning of the sentence.

```python
stripPunctuation("I don't know if I'm being productive! :(") 
> "I dont know if Im being productive"
```

### Make everything lowercase

Additionally, we found that in this particular setting, capital letters also didn’t matter that much. Because of the nature we collect our data (just a simple textbox), users tend to not bother with capitalization. As such, we remove it to make it consistent across our data.

```python
lower("I dont know if Im being productive")
> "i dont know if im being productive"
```

### Expand contractions

The English language does this weird thing where we can just smush two words together (e.g. “I am” to “I’m”). Unfortunately for us, these produce extra complexity in our model that we could reduce by making them all consistent. In our case, we chose to expand all of these contractions.

```python
expandContractions("i dont know if im being productive") 
> "i do not know if i am being productive"
```

### Remove stop words

The English language also has a bunch of these things called **stop words — **words that do not contribute anything major to the sentence in terms of semantic understanding (usually in the context of natural language tasks such as this). A few examples of them are ‘I’, ‘me’, ‘my’, ‘by’, and ‘on’. By removing them, we once again remove unneeded complexity from the model.

```python
rmStopwords("i do not know if i am being productive") 
> "not know productive"
```

### Tokenization

However, these words are not super friendly for machine learning algorithms who would much rather deal with integers and floating point numbers than words and sentences. How do we fix this?

Well, one thing we can do is turn words in indices by how often they appear, capped at the most common 1000 words — in essence, creating a vocabulary list mapping common words to numbers. For example, if “the” is the most common word, we convert it to 1. If “work” is the 8th most common word, we convert it to 8. For anything that isn’t in the top 1000, we give it the value of 0.

```python
tokenize("not know productive") 
> [12, 35, 7]
```

### Fixed sequence length

Finally, we need to ensure that all the inputs are the same length of simplicity sake. If we were to handle dynamic length inputs, it would introduce a whole other level of complexity that we’re really not ready to deal with. As such, we can make sure all the inputs are the same length by adding a bunch of zeros to those who are too short (zero padding) or by slicing those who are too long.

```python
pad([12, 35, 7], 10) 
> [0, 0, 0, 0, 0, 0, 0, 12, 35, 7]
```

### Finally

After all of these functions have been applied, we have successfully converted a complex sentence into a series of ‘tokens’ that is easy to understand for the machine learning algorithm.

```python
preprocess("I don’t know if I’m being productive! :(")
> [0, 0, 0, 0, 0, 0, 0, 12, 35, 7]
```

## What’s next?

Now that we have something ready to feed into our neural network, let’s dive into how the actual model itself works!

[Read Part 2](/posts/reflect-nlp-2)