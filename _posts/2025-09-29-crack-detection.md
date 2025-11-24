## New Use-Case for Infiniworkflow: Road Crack Detection

During our visit to Japan this September, we had the opportunity to visit the offices of a company that has contracted Photron to help with their challenges. This company, a private company that serves as a contractor for the Japanese government, manages expressways and toll roads in Japan. As part of this company's tasks, they need to scan highways for cracks and faults, outlining where all the cracks are given an input feed. Moreso, this preferably needs to be done as fast as possible, as they have to perform this scanning as a company car drives along the highway. 

A solution initially proposed to them included a massive blue-light sensor and mounting equipment that would've amounted to 1m+ per company van to install - and even then, the results that the sensor produced were not accurate enough to the company's standards.

In collaboration with Photron, we proposed a different solution - a single, high-speed streaming camera (INFINICAM) attached to the back of any car, which is connected to a laptop that is running Infiniworkflow, which would have a road crack workflow running that was built by one of the engineers at the company. Previously, this company has had to outsource coding, including code for road crack detection, to another company, which was costly and didn't yield them the results they wanted in the case of the crack detection scenario. However, with Infiniworkflow, any of the engineers at this company could design the workflow themselves, and see in real-time how well their solution works. 

Whilst in Japan, I helped create a base workflow for the engineers at the company to base their solution off of. When I returned back to the States, we realized there might be more image process techniques to help in producing an even more accurate final result.

These included techniques such as CLAHE, or Contrast Limited Adaptive Histogram Equalization, which is better than standard contrasting as it applies contrast locally by dividing up the image and equalizing the histogram on each segment. This means we can increase contrast in the crack detection workflow without washing out important details that otherwise might be lost in a general contrast approach.

![CLAHE Workflow](/assets/clahe_workflow.png)

Another technique I implemented is a new type of Edge Detection node called DexiNed, which generally yielded better results than the existing edge detection node we had (Holistically-Nested Edges).

![DexiNed Workflow](/assets/dexined_workflow.png)

(Additionally, I worked on implementing requests from one of the engineers in Photron Japan that was tasked on continuing to build up the workflow for road crack detection, which led to new nodes including Image Information and Pixel Information, which return W/H/# of channels info and RGBA/Luminance info, respectively.)

![Pixel Information Workflow](/assets/pixel_workflow.png)

And finally, here is the workflow itself for detecting and outlining cracks in roads (this is the one we built initially, not the one that the Photron Japan engineer made).

![Crack Detection Workflow](/assets/crack_detect_workflow.png)

As you can see, this solution combines tried-and-true image processing techniques with AI-based inference to create a more accurate solution than either approach could've achieved on their own. Beyond this, the benefit of Infiniworkflow is that one can see how each step of the workflow changes as users manipulate slider values in a node or change out nodes entirely, allowing for extremely rapid and fluid development.





