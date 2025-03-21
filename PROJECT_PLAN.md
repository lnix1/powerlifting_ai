
We can get a first sample case of pose estimation with the camera using the following at the command line:
```
rpicam-hello -t 0s --post-process-file /usr/share/rpi-camera-assets/imx500_posenet.json
```

But this seems to be expecting the camera is head on with the person and it overlays a square torso.

## Describing our problem

We want to develop an application for checking the position of a lifter's joints during an exercise to check that they have completed the full movement, in particular reaching depth for a squat.

So our problem is:

1) We need a dataset associating video of the lift movements with positions of the joints
	- The idea is to have the model predict the position of the joints in each frame
	- We can then draw the lines between points as we would format the model predictions in a known order (e.g. j1=right ankle, j2=right knee, etc...)
	- So the challenge is to build a dataset which gives the pixel location of each join for each frame of the video
2) Then we train our model to predict the joint positions
3) Then we package this model up and build an application script which runs the model and overlays the prediction points + drawings on the video feed

What we are trying to do is also known as "pose estimation".
For now, we want to research existing models and save the development of a bespoke dataset and model design for a later date.

## Review of existing work

For an intro to the problem of pose estimation, read here: https://medium.com/augmented-startups/top-9-pose-estimation-models-of-2022-70d00b11db43

For our purposes, kinematic pose estimation most accurately describes our poblem since joint position is what we want to estimate.
In particular, we want to draw a line between the core of the knee and the hip to ensure the lifter's hip drops as lows as the center of the knee.

A solid and modern choice appears to be TransPose (2021):

- Github: https://github.com/yangsenius/TransPose?tab=readme-ov-file
- Arvix: https://arxiv.org/abs/2012.14214
- Youtube: https://www.youtube.com/watch?v=HsBdmJYJs74

An additional choice appears to be PCT (2023):

- Arvix: https://arxiv.org/pdf/2303.11638v1

## Jan. 20th, 2024 Update

The primary documentation for working with the camera is here: https://www.raspberrypi.com/documentation/accessories/ai-camera.html

There are basically two options for working with the camera: rpicam-apps, and Picamera2

- The first requires writing .cpp files for deploying any model, parsing results, and overlaying on video feed.
- The second has everything I need, can be done all via python, and seems to run just as smooth for smaller models.

We'll go with Picamera2.

### Updated project plan

I want to build a project which allows me to do all of the following:

- Create & annotate video files
- Specify a model architecture
- Train the model on the annotated files & save out the result
- Quantize & compress the trained model, convert compressed model to IMX500 format, and package the converted file into a firmware file that can be loaded at runtime onto the camera
- Deploy model to camera and run a video application which plots results of model inference to the video

These steps break out into a few applications. We will develop each with the specified success criterion:

- [ ] Application for compression, conversion, and packaging of a trained model.
	- Success criterion: application started from the command line takes flags for trained model path & output path, then produces firmware file. First tests will just use a pre-existing model.
- [ ] Application for training a model from annotated video files.
	- Success criterion: application started from the command line takes flags for path to folder of annotated videos & model architecture specification & output file path, trains model, saves trained model to output file. 
- [ ] Process for annotating video files.
	- Success criterion: I will be using CVAT, so success here is simply installing and learning to use the tool on my personal machine.
- [ ] Application for starting up the camera with model firmware path specified and producing output video file with model results overlaid.
	- Success criterion: application started from the command line with model firmware path specified which uploads the model, starts the camera, and overlays model results over video feed.

Further areas to build after MVP:

- Saving video file with model results overlaid.
- Easy start-up and stop of python application. Perhaps integrated with a clicker button via USB.
- Automating video retrieval and labeling / annotation of training & test data.

## Further Research (March 15, 2025)

### Other attempts at the same task

Other attempts have been made at form estimation for powerlifting / weight training to create [automated tooling for form supervision](https://arxiv.org/pdf/2202.14019). However, I have found only two attempts at explicitly automating depth judging:

1. [Automated Powerlifting Judging through Keypoint Detection](https://cs231n.stanford.edu/2024/papers/automating-powerlifting-judging-through-keypoint-detection.pdf)
2. [ATG.AI](https://github.com/RanGlad12/ATG.AI)

I will use the first to inform the system I build and the second to avoid potential pitfalls related to camera angle. For example, I originally intended this project to cover only a side view of the lifter and judge depth from either a right or left perspective. On review of ATG.AI's attempt at this same tooling, I realized that spotters would almost completely obscure this perspective. Instead the angle will have to be from either slightly behind the lifter on the left / right, or directly head-on.

### Building a Dataset

Similar to paper number one above, I will use publically available YouTube videos from prior meets. However, I intend to manually label the videos as my goal is to learn the process in this project. This means I will construct a smaller dataset and will not initially re-create their data pipeline approach. Creating an automated labeling pipeline will remain a future point of expansion though.
