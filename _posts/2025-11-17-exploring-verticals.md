## Exploring New Verticals for Infiniworkflow

The advent of us beginning to roll out Infiniworkflow to real customers has led to a lot of positive rapid momentum in building IW. With these changes, we realized that we needed to switch gears from thinking about which nodes to add to thinking about which verticals we could support in Infiniworkflow, so over the last 2 weeks my principal task has been to create complete, end-to-end workflows for different verticals. Here are just a few of the workflows I've made so far.

Welding Analysis - takes in welding footage (provided to us by one of the engineers from Japan working on CamMonitor) and performs Dense Optical Flow (which is now significantly faster thanks to CUDA speedup). A BW version of that footage and a mask are combined with Bitwise And to generate a predominantly black image where white pixels only appear if any welding happens outside of the designated mask I made with Quick Path. This is fed into Statistics for Non Zero Pixels, which tells us the number of white pixels at any time; if the total number of white pixels is greater than a threshold acceptable value, then we get an output of True - this could then be fed into another node to save out footage whenever the output is True, i.e. when the welding is messed up and welding happens outside of the acceptable area.

![Welding Analysis](/assets/workflow_welding_analysis.jpg)

Security - takes in footage from outside a prison. Mask Inference is used to detect people in the scene, and Quick Path outlines the top of the prison fence. These outputs are combined with Bitwise And and then fed into Grayscale Statistics - if the number of white pixels is too high, this means a person is hopping the fence, so an alarm is sounded via Sound Trigger.

![Security](/assets/workflow_security.jpg)

Line Feeder Analysis - takes in footage from a line feeder. We use Time Sample 2D to put a line (the horizontal green one) to see if any chips on the line feeder accidentally pop up (like the one seen in the snapshot). CIELAB Threshold gets us a BW version of the output of Time Sample 2D, which scans all pixels that are on the line and stacks them 1 line at a time in the output, so that you can see a history of pixels moving over time. We feed in the mean pixel value into a Time Sample 1D node to give us a table of mean pixel values, which we then feed into a line plot to get the output you see in the snapshot.

![Line Feeder Analysis](/assets/workflow_line_feeder.jpg)

Crowd Motion Tracking - takes in sped-up, top-down footage of the lobby of a large train station, and feeds it into Mask Inference to detect all people in the scene. We can get the number of people in the scene already as an output, or we can feed the Preview output into Dense Optical Flow, and multiply that by the Mask output of Mask Inference, to get a really cool result - dense optical flow applied only to the people in the scene. This is then fed into Grayscale Statistics and Time Sample 1D to get a table of the mean pixel values in the output image, i.e. a table that shows how fast people are moving in the scene (as the speed of an object changes its color in the output of dense optical flow). This means crowd rushes could be detected and logged whenever they happen.

![Crowd Motion Tracking](/assets/workflow_crowd_tracking.jpg)

Car Movement - takes in footage shot from a car driving in downtown LA, and feeds it into Mask Inference to only detect cars in the scene. By combining Delay and Absolute Difference (as well as an Erode to clean up the output), we can see that a white outline surrounds any car that moves - slight movement will only have a small amount of white pixels on screen, whereas rapid movement will have a larger amount of white pixels. We can then track the mean pixel value of the image (i.e. how fast cars are moving in the scene / how rapidly they are changing direction) using Grayscale Statistics and a Time Sample 1D node.

![Car Movement](/assets/workflow_car_movement.jpg)






