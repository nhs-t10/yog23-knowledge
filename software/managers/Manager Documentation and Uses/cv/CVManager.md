# CVManager

## CVManager Overview
CV is computer vision. To utilize it, create a pipeline (documentation at software/cv/making-a-pipeline.md). That goes into the nitty-gritty of cv processing (or it will, at least), so this is more about CvManager itself, being the integrating bridge between the two. This includes:
1. Common errors, and how to fix them (please add your own as you find them).
2. Initializing the camera
3. Calling pipeline functions (It's more complicated than it sounds. Seriously. This caused ~1/2 the bugs I had to fix when learning about CV)
4. Which of the many functions you can ignore. I'll be trying to clean those up, but you may have to finish the job.

## Common Errors (1) (Please skip this until you understand parts 2 and 3, or this will confuse and befuddle you)

**MAKE SURE THE CAMERA IS INITIALIZED! See section 2.**

If your CV is printing nothing, or weird results, when you do telemetry.log(output):
  - Make sure your camera is oriented properly (I recommend using the phone to view the camera stream - three dots in the top-left. Use the imgproc.rectangle command. See old pipelines for examples.)
  - Check the robot configuration. Is the camera named Eyer, and in the right location?
  - Make sure that your constructor's pipeline_index value is the right thing, and that the three pipelines at the top are also right.
  - Make sure that your function call matches the initialized pipeline

## Initializing the Camera (2)

Before using CV, you have to initialize the camera. Run webcam.startStreaming(640, 480, OpenCvCameraRotation.UPRIGHT) or cv.onOpened(). The first two parameters are resolution, and the last is orientation. 
More information at https://github.com/OpenFTC/EasyOpenCV/blob/master/doc/user_docs/camera_initialization_overview.md


## Pipeline Functions (3)

Pipelines have three essential functions: processFrame, getAnalysis, and getAnalysisPrecise. 

processFrame takes as input the camera feed and outputs whatever it does - but only when you run getAnalysis or getAnalysisPrecise. You *never* have to run processFrame manually.

getAnalysis returns an int. This int is not premade, you must create and change it yourself. I recommend changing it in processFrame.

getAnalysisPrecise returns a double. Same deal as with getAnalysis.


## Important Functions (4)

Except or the ones you write yourself, the only important functions are the six that return unedited getAnalysis and getAnalysisPrecise form the three pipelines. The others are outdated relics.
