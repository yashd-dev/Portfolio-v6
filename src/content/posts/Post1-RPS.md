---
title: Making of Rock Paper Scissors Using OpenCV and Mediapipe
description: "My Experience in building this project!"
image:
    url: "/RPS-Screenshot.png"
    alt: "Preview of My Game"
pubDate: 2023-11-16
---

## Why make it?

I made this game simply for the purpose of learning about OpenCV and as my semester end Python project. The game is simple and straight forward and the codebase is also the same. It sure was a headache to make, especially implementing MediaPipe because Google's documentation was a bit difficult for me to understand and other tutorials out there were not aligning with my vision for this project.

[**_Here is the codebase for my project._**](https://github.com/yashd-dev/RPS-using-OpenCv) I have documented each and everything as comments in the Jupyter Notebook itself. If I have missed out on something, you could open an issue or pull-request on Github or email me about it.

## Working of The Game

Unless you live under a rock, you must know about the simple game of Rock Paper Scissors.

> For the uninitiated, click here to know more about the game

My implementation of this game is in Python which uses OpenCV , a real-time computer vision library, to capture the player's hand gestures through a webcam and applies MediaPipe , a library of AI/ML models on the captured data to recognize the hand and its movements. The system then classifies the hand gesture as either rock, paper, or scissors using hand landmarks and their coordinates. The PC's move is randomly generated

Thats a loads of stuff in one paragraph, ill quickly break it down for you :)

## What OpenCV Does:

!["Matrix"](/matrix.png)

OpenCV reads from the webcam and stores each frame as a matrix of BRG (Blue, Red, Green) values of each pixel of the image. BRG is essentially RGB (Red, Green, Blue) values but reversed. OpenCV reads in images in BGR format instead of RGB because when OpenCV was first being developed, BGR color format was popular among camera manufacturers and image software providers. The red channel was considered one of the least important color channels so was listed last. However, now the standard has changed and most image software and cameras use RGB format,due to better image quality.

## What Mediapipe Does

Mediapipe is basically a pre-made AI/ML solutions/modals which Google has made available to the general public for free.It provides a variety of pre-built, customizable solutions for various use cases like object tracking, audio classification.I used the Hand Gesture Recognition Solution which uses the hand landmark model. The hand landmark model bundle detects the key-point localization of 21 hand-knuckle coordinates within the detected hand regions. The model was trained on approximately 30K real-world images, as well as several rendered synthetic hand models imposed over various backgrounds.

!["Matrix"](/hand-landmarks.png)

## Making them work together

OpenCV passes each frame to MediaPipe for analysis of the frame and predicting the hand landmark co-ordinates. My Code logic goes as follows:

From the detected hand, we extract the y axis value of the TIP of the finger and the PIP of the finger (look at the diagram below for better understanding). Note I am excluding the thumbs to reduce complications ie taking both x and y axis and comparing both. Also the wrist is the origin point of the axis

!["Matrix"](/handlocations.png)

Now that we have y axis values of all fingers, we'll compare them. In digital images, the height increases top to bottom and width increases right to left.Here we are dealing with just the height.

Now For Paper Hand Gesture, TIPs will be above the PIPs, hence the value of TIP.s will be lower than the PIP's.

The opposite is true for Rock Hand Gesture , TIPs will be below the PIPs, hence the value of TIP's will be higher than the PIP's.

For the Scissors, the TIPs will be above the PIPs for just the index.

There are many exceptions i did not take into account simply because i was short on time. Like if paper gesture is made horizontally, it wont work as the TIP's align with the PIP's making them equal. Hence you would have to compare them along the x axis. Similar issues can be found.

## Difficulties I faced

-   Understanding MediaPipe:
    It was difficult for me to understand the documentation, I guess Im not smart enough to understand it for now. Some youtube videos certainly helped me to understand it better!

-   Not many Guides:
    Not many guides were available so relying on documentation was my only option :)

## Conclusions

Well I got full in my project so thats nice. I have also learnt to rely more on documentation and keeping patience!
