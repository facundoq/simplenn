


#  `simplenn`

## :brain: Learn how modern, modular Neural Networks work by implementing a PyTorch/Keras-like framework.

`simplenn` is a very simple library that contains the basic elements to define, train and use **modular** Neural Networks using just Python and Numpy ([full example](https://colab.research.google.com/github/facundoq/simplenn/examples/iris_classification.ipynb)).

````python
import simplenn as sn
x,y = load_data()
din,n_classes=4,10
layers = [sn.Linear(din,10),
          sn.Bias(10),
          sn.ReLU(),
          sn.Linear(10,n_classes),
          sn.Bias(n_classes),
          sn.Softmax()
          ]

model = sn.Sequential(layers)
print(model.summary())
error = sn.MeanError(sn.CrossEntropyWithLabels())
optimizer = sn.GradientDescent(lr=0.1,epochs=3000,batch_size=32)
history = optimizer.optimize(model,x,y,error)
sn.plot.plot_history(history)
````

We _remove_ the key parts of `simplenn` that deal with layers, initializers, error functions, backpropagation and optimizers. Then, through our guides, we help **_you_ reimplement** the key parts of `simplenn`. We also provide various automated tests along the way for you to check your solutions. 


Supported languages:

* [Spanish](https://github.com/facundoq/simplenn/blob/main/releases/simplenn-es.zip)
* English (coming soon)


## :rainbow: Why `simplenn`?

There are many excellent courses or books that teach you how to program neural networks from the ground up such as [*CS231n: Convolutional Neural Networks for Visual Recognition*](https://cs231n.github.io/), Andrew Ng's [*Machine Learning*](https://www.coursera.org/learn/machine-learning) or Sebastian Rascha's [Python Machine Learning](https://sebastianraschka.com/books/#python-machine-learning-3rd-edition). However, while these are great for understanding the basics using `numpy`, they use monolithic neural network models that make it difficult to understand how that code translates to other frameworks such as `pytorch` or `tensorflow`.

Alternatively, [Andrew Ng's *Deep Learning*](https://www.coursera.org/specializations/deep-learning) or [*FastAI*](https://course19.fast.ai/part2) build modular networks out of `tensorflow` or basic `pytorch` operators instead of numpy. This is great to build complex models quickly, but there's still a lot of magic under the hood. Both frameworks automatically derive `backward` methods and bring along other goodies. 

Reimplementing `simplenn` allows you to understand how modern neural networks frameworks work and fills the gap between those types of learning. You get to program a full neural network framework, without all the magic `pytorch` or `tensorflow` bring along. Of course, `simplenn` does help you out along the way and provides many 


## :heavy_plus_sign: Pre-requisite knowledge

The guides are intended for learners with some experience with Python, Numpy and Neural Networks. We have included explanations of what you should implement, but learners still should be able to:

1. Read and write object-oriented python code, including subclassing and method overriding.
2. Understand Numpy, basic linear algebra and calculus and be able to translate  mathematical operations to Numpy code.
3. Understand the basic ideas in modern modular Neural Network frameworks, such as models, layers, optimizers, batches, backward and forward passes, and specially backpropagation. It is also helpful to have previous exposure to `tensorflow/keras` or `pytorch`, but not necessary.

## :wrench: Download and setup

**Do not clone** this repository if you want to use `simplenn` as a learning exercise. Instead use the following instructions. These instructions assume a working installation of python3 (3.6 or greater), pip3 and virtualenv. The installations of those varies wildly with OS/distribution so its up to you to get a setup working. Afterwards: 

1. Download a [release](https://github.com/facundoq/simplenn/blob/main/releases) for your language. If you prefer the command line, use `wget`, replacing `es` with your preferred language (only `es` currently supported):

    `wget https://github.com/facundoq/simplenn/blob/main/releases/simplenn-es.zip`

2. Unzip to `simplenn` or other folder name you choose:

    `unzip es.zip -d simplenn && cd simplenn`

3. Make sure Python3.6 or greater, pip3 and venv are installed:

    ````bash
    python3 --version
    pip3 --version && 
    python3 -c "import venv" && echo "venv is installed"
    ````
   

4. Create a virtualenv environment and install the dependencies in the requirements file `requirements.txt`: 

    ````bash
    python3 -m venv nnenv
    source nnvenv/bin/activate
    pip install -r requirements.txt
    ````

Alternatively, you can use your `conda` distribution or another such tool to create a virtual environment and install the required libraries for `simplenn` (listed inside `requirements.txt`). 

5. Run jupyter and follow the guides:

```bash
jupyter notebook
```

## :pill: Solutions and bugs :bug: 

`simplenn` is designed so that you can automatically test your implementations. However, it is intended to be used as a set of exercises in a course or seminar. Please address all questions regarding the material to your instructor.

This repository also has a [reference implementation](https://github.com/facundoq/simplenn/tree/main/simplenn) in the `simplenn` folder of the library you can consult. 

Alternatively, you may consult public forums such as [stack overflow](stackoverflow.com/), [r/neuralnetworks](https://www.reddit.com/r/neuralnetworks/) or [r/MachineLearning](https://www.reddit.com/r/MachineLearning)

Please, **only [file an issue](issues) if there is an actual bug** or feature request, not if you can't solve the exercises.  

## :package: Reference implementation and usage as library


You can `pip install simplenn` to use the reference implementation of the library to train models and use them. Indeed, the API is very simple:

````python
import simplenn as sn
x,y,n_classes = ... # load data 
n,din=x.shape

# Model definition
layers = [sn.Linear(din,10),
          sn.Bias(10),
          sn.ReLU(),
          sn.Linear(10,20),
          sn.Bias(20),
          sn.TanH(),
          sn.Linear(10,n_classes),
          sn.Bias(n_classes),
          sn.Softmax()
          ]

model = sn.Sequential(layers)
print(model.summary())

error = sn.MeanError(sn.CrossEntropyWithLabels())
optimizer = sn.StochasticGradientDescent(lr=0.001,epochs=1000,batch_size=32)
history = optimizer.optimize(model,x,y,error)
````

However, we **do not recommend** doing so since the library is *slow* and not meant for neither research nor production environments. The reference implementation is mostly focused on being easy to understand so that learners can check their implementations.

## :busts_in_silhouette: Contributing

We'd like your help to expand `simplenn` with more guides/layers/optimizers. Check out our [contribution guide](CONTRIBUTE.md)! 
