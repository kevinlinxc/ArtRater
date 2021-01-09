# ArtRater
## Project Description:
This project is an attempt to create a Convolutional Neural Net that predicts how many upvotes a picture posted on Reddit r/art would get.

I was hoping that in using a CNN, I could identify features that highly upvoted posts have.

The main tool used is **Tensorflow/Keras**, and pictures were downloaded from Reddit for training using **PSAW** (PushShift API Wrapper) and **PRAW** (Python Reddit API Wrapper)

The neural net ended up not training too well, with the accuracy plateauing around 25%. I'm not sure
if it's because it's naturally hard to find a pattern that highly rated posts share, or if it's a flaw in my implementation of the convolutional layers.

It also doesn't help that so many posts, regardless of quality, get stuck at 0 or 1 upvotes on Reddit, and so it would make sense if my neural net only wanted to guess 1 for every input.

ALl in all, this project was a learning experience for me, and it taught me that variable input size and creating my own dataset are possible.

## Quick start info
The main Jupyter notebook I used is main.ipynb, and the noteboook that I adapted for training on Google colab is colab.ipynb

The path names for the folders where images were downloaded/processed from have been changing as I've been prcoessing different pictures. Change them for your own usage. 


## Preprocessing
Since I downloaded images from Reddit, some preprocessing was necessary. I had to:

1. Detect and delete corrupt/images deleted by Reddit
2. Convert grayscale images to colour so that every image has 3 channels
3. Remove alpha channels if those existed
4. Scale images down to 1000 pixels on a dimension max so that my computer could actually train in a reasonable amount of time


## Custom file generation
Since I was trying to train on over 20000 pictures, it wasn't possible to load them all into memory, so I instead made a custom
image generator custom_file_image_generator to feed pictures to Keras.fit one at a time. This required storing the names of files
from my training and validation set into .txt files so that I could follow [this tutorial](https://www.pyimagesearch.com/2018/12/24/how-to-use-keras-fit-and-fit_generator-a-hands-on-tutorial/)
I ended up resizing the files anyway to make training shorter/make be able to upload the pictures to Google Drive, so maybe loading them into memory was viable now, but this was a good
learning experience in not having my hand held in terms of dataset processing.


## Variable image input size
Another quirk that I wanted was the ability to input pictures of varying shape, rather than a set input shape.
This was achieved using GlobalMaxPooling and following the steps in [this Stack Overflow post](https://stats.stackexchange.com/a/445201).
Again, it could be that my network isn't learning because of this quirk I tried to implement.

## Other notes
I'm using a layer in the neural net to normalize the pictures to [0 1]

I've tried normalizing the scores to [0 1] or just leaving them as [0 maxscore], but no success
