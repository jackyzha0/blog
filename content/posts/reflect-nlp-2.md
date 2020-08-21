---
title: "reflect: NLP model explained pt.2"
date: 2020-05-10T08:51:56-07:00
---

How do we tell that this is a “valid” intent?

In this second part, we’ll take a deep dive into the neural network that helps us solve this hefty problem of classifying whether an intent is valid or not.

Recall that in part 1, we went over the data we had, and how we could prepare that data to feed into our neural network. Now that we have all our data ready and prepped, let’s talk about the model!

## The model

The type of neural network that we’ll be using is called Long Short-Term Memory (LSTM).

![credit: Christopher Olah, 2015](https://cdn-images-1.medium.com/max/4000/0*HyoZq6fOfsnn2YOC)*credit: Christopher Olah, 2015*

What’s so special about these networks is that they are really good at modelling time-series data, making it an ideal candidate for tasks like forecasting or natural language processing.

```python
# Function to create a RNN model with given parameters
# max_seq_len: maximum token sequence length
# vocab_size:  size of tokenizer vocabulary
def RNN(max_seq_len, vocab_size):
    inputs = Input(name='inputs', shape=[max_seq_len])
    layer = Embedding(vocab_size, 64, input_length=max_seq_len)(inputs)
    layer = LSTM(64, return_sequences = True)(layer)
    layer = Dropout(0.5)(layer)
    layer = LSTM(64)(layer)
    layer = Dense(256, name='FC1')(layer)
    layer = Dropout(0.5)(layer)
    layer = Dense(1, name='out_layer')(layer)
    layer = Activation('sigmoid')(layer)
    model = Model(inputs=inputs, outputs=layer)
    return model
```

Here’s how we define it in our [Keras code](https://github.com/jackyzha0/reflect-nlp/blob/master/nlp/net.py), don’t worry if you don’t understand it just yet! We’ll explain it in the next few paragraphs.

```python
inputs = Input(name='inputs', shape=[max_seq_len])
```

Right off the bat, you’ll notice that the first layer is the Input layer. Basically, this tells Keras to instantiate a new tensor (a multi-dimensional vector) with a given shape. In this case, we’re creating a one-dimensional tensor that is max_seq_len units long. When we trained our model, this was set to 75.

```python
layer = Embedding(vocab_size, 64, input_length=max_seq_len)(inputs)
```

Next up, we have the Embedding layer. We could get into a really technical discussion about what this really does, but you can think of it as a layer that helps the neural network to learn semantic relationships between inputs.

![credit: Rutger Ruizendaal, 2017](https://cdn-images-1.medium.com/max/3010/0*YOZ_CfmtgpUbJ9BD)*credit: Rutger Ruizendaal, 2017*

Essentially, it embeds tokens in a higher dimension vector space, where distance between tokens represents its similarity.

```python
layer = LSTM(64, return_sequences = True)(layer)
```

Now, we get into the meat of the neural network: the LSTM layer. As stated before, these LSTM networks are really good at modelling time series data like language. In this case, our LSTM network has 64 hidden units per cell, and that we’d like to pass these hidden states to the next layer. If you’d like to learn more about the inner workings of the LSTM model, theres a really good resource [here](https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21)!

```python
layer = Dropout(0.5)(layer)
```

Next, you’ll notice there are a few Dropout layers. These layers help to prevent overfitting by randomly killing off connections between the two layers (a sort of regularization). This makes sure neurons aren’t just “memorizing” the input data. This is especially important because our dataset is relatively small (~2000 observations even after augmentation), so making sure that our machine learning model can generalize outside of this limited dataset is really important.

```python
layer = LSTM(64)(layer)
```

We have yet another LSTM layer! By having these two chained right after each other, the first layer can pass all the values of all of its hidden states to the second layer, effectively allowing a sort of ‘deeper’ neural network.

![credit: Jianjing Zhang 2018](https://cdn-images-1.medium.com/max/2000/0*0BRdnA5sJBYbaeR9)*credit: Jianjing Zhang 2018*

This deep LSTM allows our network to learn more abstract concepts, making them well suited for natural language tasks.

```python
layer = Dense(256, name='FC1')(layer)
```

Next, we have something called a Fully Connected layer, or a Dense layer. In a dense layer, each of the input neurons is connected to every output neuron. This kind of ‘glue’ layer helps the network to pick out and discriminate feature output by our previous LSTM layer.

```python
layer = Dense(1, name='out_layer')(layer)
layer = Activation('sigmoid')(layer)
```

Similarly, we have one final Dense layer that ‘compresses’ all of the hidden units down to one neuron. However, we want the output value of this neuron to be how confident from a scale of 0 to 1 it is that the intent is valid. We do this by applying something called an activation function.

![A sigmoid activation function](https://cdn-images-1.medium.com/max/2000/0*kdowh3GOGOUvGBr0)

In this case, the particular function we chose is the sigmoid activation function, which looks something like the above.

### Model Overview

Phew, finally got through everything! After putting it all together, we end up with a network that looks something like this:

```python
# 75 max_seq_len
# 1000 tokenizer_vocab_size
model = net.RNN(75, 1000) 
model.summary()

# _________________________________________________________________
# Layer (type)                 Output Shape              Param #   
# =================================================================
# inputs (InputLayer)          (None, 75)                0         
# _________________________________________________________________
# embedding_1 (Embedding)      (None, 75, 64)            64000     
# _________________________________________________________________
# lstm_1 (LSTM)                (None, 75, 64)            33024     
# _________________________________________________________________
# dropout_1 (Dropout)          (None, 75, 64)            0         
# _________________________________________________________________
# lstm_2 (LSTM)                (None, 64)                33024     
# _________________________________________________________________
# FC1 (Dense)                  (None, 256)               16640     
# _________________________________________________________________
# dropout_2 (Dropout)          (None, 256)               0         
# _________________________________________________________________
# out_layer (Dense)            (None, 1)                 257       
# _________________________________________________________________
# activation_1 (Activation)    (None, 1)                 0         
# =================================================================
# Total params: 146,945
# Trainable params: 146,945
# Non-trainable params: 0
# _________________________________________________________________
```

Theres a grand total of 150,000 different trainable knobs and parameters in our neural network!

## Training pipeline

So, how does the data we got earlier play a role in helping our machine learning model learn and improve?

The first component is the **loss function.** This component tells the neural network how ‘correct’ its prediction was. In this model, we will use something called [binary cross entropy](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a), which is basically a fancy word for log-based error. If the true label is 1, we can then show what the log-loss would be for some given prediction probability.

![](https://cdn-images-1.medium.com/max/2000/0*8rd4ho_3Y6zrtra-.png)

Next, we need to pick an **optimizer**. This component tells the neural network how to change its parameters to improve or ‘optimize’ itself. In this model, we chose to use an optimizer called [RMSProp](https://towardsdatascience.com/understanding-rmsprop-faster-neural-network-learning-62e116fcf29a) with a learning rate of 1e-3 . We aren’t going to cover all the technical details of this optimizer in this blog post, but just know that it is a very fast and effective optimizer.

![RMSProp(black) vs a bunch of other optimizers. credit: Vitaly Bushaev](https://cdn-images-1.medium.com/max/2000/0*HZM5XJ-quu276w39.gif)*RMSProp(black) vs a bunch of other optimizers. credit: Vitaly Bushaev*

One important hyperparameter we choose is the **train-test split.** In data science and machine learning, we typically withhold part of our data and set it aside as a **test set**. The rest of the data will be considered the **training set.** When training the model, we never feed it the test set. As a result, we can use the test set as a metric to see how well it would perform on real-world, unseen data. In our training, we used a train-test split of 20%.

Another important hyperparameter that we can choose is the **mini-batch size**. The mini-batch size determines how many training examples we feed the machine learning model before updating its parameters. A smaller mini-batch means that we get more frequent updates to the parameters, but it also runs the risk of having outliers that may cause a bad gradient update. A large mini-batch means that we get a more accurate gradient update but it also takes longer. A similar concept is *sample size* in statistics. We could pick a larger sample to get a better estimate of the overall population, but it is often more expensive to do so. A smaller sample might contain outliers and thus be less robust of an estimate of the overall population, but it very easy to do. So, there’s this tradeoff between accuracy and speed. We found that a good balance between these was a mini-batch size of 128.

We then trained our neural network over 10 epochs. A single epoch is one iteration over the entire dataset. If we train it for too many epochs, you run the risk of overfitting (memorizing the training data), but we don’t train it enough, we run the risk of not discovering a better model. One thing we can do it minimize this problem is through the use of cross-validation, which is a technique that lets us ‘test’ on portions of the training set. Essentially, at each iteration during training, we withhold a portion of the training set and use it as a sort of ‘validation’.

![credit: Raheel Shaikh](https://cdn-images-1.medium.com/max/2000/0*6XoMgZUd3SxXgqBj.png)*credit: Raheel Shaikh*

By seeing when this validation accuracy goes down, we can get a pretty good idea of when our model begins to overfit on our data, and stop the training before this happens. In training our model, we will use 5-fold [cross-validation](https://towardsdatascience.com/cross-validation-explained-evaluating-estimator-performance-e51e5430ff85).

After all of this, we end with a training accuracy of 93.60% and test accuracy of 85.95%. Not bad at all!

## Serving the model

Great! So now we have a trained model. Can we put that in the Chrome extension now? Not quite yet…

Our model was written and trained with Keras (a Python Deep Learning library). Our Chrome extension is written in TypeScript. How do we get these two to work together?

Luckily for us, Tensorflow.js exists! This library allows us to run Tensorflow models from within JavaScript. Tensorflow has released a script that lets us to convert a Keras model into something that Tensorflow.js understands, so we can run that to convert our models.

However, we can’t just directly plug-and-play. You may remember that we did all of that data preprocessing before we trained our model. Tensorflow.js doesn’t have any of this built in, so we made our own implementation of it. You can check it out [here](https://github.com/jackyzha0/reflect-chrome/blob/master/src/nn.ts).

We’ll leave all the technical code out (if you’re interested, feel free to peek around the source code!), but we’ve abstracted it enough that classifying an intent is a breeze.

```typescript
// declared somewhere earlier
const model: nn.IntentClassifier = new nn.IntentClassifier("acc85.95"); // name of converted model

// send to nlp model for prediction
const valid: boolean = await model.predict(intent);
if (valid) {
    // let through
} else {
    // block page
}
```

## Future improvement

### Possible models

We have thought about using something more established and complex like [BERT](https://arxiv.org/abs/1810.04805) and retraining it on our dataset, however then comes the problem of runtime and memory usage.

BERT is a huge model. If you thought 150 thousand parameters was a lot, wait till you see BERT’s 110 *million* parameters. This bad boy takes a few hundred times longer and many times more memory than our current model. While yes BERT may perform really well, we just don’t think it has a place inside of a Chrome extension.

Our model is decently robust as it is, especially considering the entire model is <2MB and takes less than 200ms to run in browser. For now, we will stick with lightweight models, but we may switch if we find a better match in the future :)

### Misclassifications

Of course, this algorithm isn’t perfect. It does have a lot of flaws and weaknesses that we find every day, and we’re working to fix those! If there are any misclassifications that you find in the algorithm, we love to hear about it on our feedback form: [https://forms.gle/ctypb6FmDT9RQqjv6](https://forms.gle/ctypb6FmDT9RQqjv6).

## Closing

This NLP model is at the core of reflect. It is this model’s goal to predict whether user intents are valid or not. As a result, we need to make sure this algorithm is accurate, fast, and lightweight. Hopefully, through this blog post, you’ve learned a little about how we went about building a model to fulfill those requirements.

Learn more about us on our website! ✨ [http://getreflect.app/](http://getreflect.app/)

If you have any further questions about reflect or this NLP model, feel free to shoot us an email at hello@getreflect.app

[Read Part 1 if you haven’t already!](/posts/reflect-nlp-1)
