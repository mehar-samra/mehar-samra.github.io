## Infinicam Save Integration in Infiniworkflow

INFINIWORKFLOW was designed to be a platform for streaming in high-speed data. Hence, of the various high frame rate cameras that Photron sells, the newly launched INFINICAMs are the ideal candidate for extensive integration / support in INFINIWORKFLOW. 

The integration was developed with the needs of a high value client in mind, who stated that they wished to deploy several INFINICAMs across a factory floor to monitor for mistakes, and record when the mistakes occur. Under their current system, their cameras are recording constantly, which means an agregious excess of recorded material, when in reality they only need to record the time just before and just after the incident occurs on the factory line. This is where the Photron USA engineering team came in.

I was tasked with the majority of the development, including making a buffer manager (so that we only store a select number of frames at a time, that we then save out if the Save Infinicam trigger is pushed), and a node for saving the videos as well.

The buffer (and system as a whole) operates very similarly to the project I developed in my first internship (reference older blog post). The buffer manager had a preroll and postroll (i.e. the number of frames before and the number of frames after the trigger is pushed that will be saved, respectively), with the buffer length being the sum of the preroll and postroll. Once the trigger is pushed and saving is underway, we switch to a different thread to perform the slow task of saving out all of the frames in the buffer. This way we do not impare the extremely high performance of the INFINICAM, and allow for multiple saves to happen in succession if the user chooses.

Separately, we have the Save Node, which has the controls for triggering the save, setting the playback FPS, the delay between saves, and more. A workflow for using the save node would look something like this:

![INFINICAM Workflow](/assets/infinicam_workflow.jpg)

Above, we have the INFINICAM feeding into a YOLOv5 detection node, which has been set to only detect people, and if the number of people in the scene is greater than 0, we save out the footage. Here is what the saved footage looks like:

![Saved INFINICAM Footage](/assets/infinicam_demo_patch_update.gif)

This was an extremely important development for the INFINIWORKFLOW team, as multiple teams within and beyond Photron have wanted to use INFINICAM to perform various tasks (saving, detection & tracking, etc.) that INFINIWORKFLOW can do with ease.



