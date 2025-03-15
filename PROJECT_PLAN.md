
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
- [ ] Application for annotating video files.
	- Success criterion: TBD, (I currently have no clue what annotating entails but will update this when I research more)
	- I have some thoughts about automating this portion by using stickers of a wild color stuck to a lifter and another existing model to then automatically generate the pixel locations in the video file to generated annotate "joint" locations.
		- In this case, this would mean loading new video files to the raw file folder, running the color-based model to output files with the pixel location data.
- [ ] Application for starting up the camera with model firmware path specified and producing output video file with model results overlaid.
	- Success criterion: application started from the command line with model firmware path specified which uploads the model, starts the camera, and overlays model results over video feed.

Further areas to build after MVP:

- Saving video file with model results overlaid.
- Easy start-up and stop of python application. Perhaps integrated with a clicker button via USB.
