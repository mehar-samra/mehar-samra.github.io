## Welding Analysis with Infiniworkflow

A former member of Photron is now working with a company that is attempting to do close analysis of welding in factories, to ensure that there are minimal mistakes or errors. Photron had a propietary system for welding analysis, but more needed to be done -- the company needed more than just statistical readouts, but accurate models they could use to identify welding defects in real-time. This is where Infiniworkflow is coming in as a tool for these researchers to use.

Firstly, I needed to integrate this older system into Infiniworkflow, which required much more than simple copy and pasting, as the old system had its own system of threading that is quite different to the one Infiniworkflow uses to achieve its high level of performance. Additionally, in order to prevent one node from being extremely complicated, I split this node into 5 different nodes: a Welding Preprocessor for common tasks and 4 Monitoring Nodes for determining the Bead Width, Spatter, Pool Area, and Hole/Pit Defects in a weld. Thanks to CUDA acceleration, these nodes run with very high performance.

![Welding Quality Workflow](/assets/welding_quality_workflow.png)

However, in order to achieve better results for the team, we needed the ability to take in video data and label it to create a custom dataset for detection/segmentation training. We already had the initial workings of the AI Labeling system in Infiniworkflow, but we expanded it further: we allowed videos to be accepted as an input, which would then be split up into frames, which could then be labeled by hand with our useful Pathing system, or use SAM2 from Meta to automatically label the data, or import pre-labeled image data. 

However, when we tried to use SAM2 for automatic labels, the labels were decent at best and entirely incorrect at worst at determining which parts of the image were part of the weld and which weren't. As such, we decided to implement video propogation. This meant instead of having to label all of the frames of an input video to have a complete dataset for training, you could instead label a few images across several hundred total frames, and then use SAM2 to intuit what the segmenation should be in all the frames in between. This provided remarkably better results in the training data, which then meant we had much better AI Inference models to be able to use in real-time settings for welding machines.

In this test example, we are segmenting and labeling the Welding Tip in a short video, with the image showing what the loading screen looks like as the automatic video propogation labeling is occurring.

![SAM2 Video Propogation](/assets/sam2_video_propogation.png)










