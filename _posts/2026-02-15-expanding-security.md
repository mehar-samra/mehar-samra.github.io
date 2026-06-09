## Expanding Possible Security Applications inside Infiniworkflow

Of the many possible verticals that we could target, the one that we are currently looking to start with and expand on is security, specifically security for corporate or construction sites. Below are just a few examples of some of the more interesting nodes I got to develop:

Line / Region Crossing - flow monitoring of detected objects (typically people if in a crowd setting, such as an airport or corporate building entrance), which can either be done over 2 distinct points, or in a region as dictated by a Quick Path node. (In Line Crossing we detect how many people/objects flow in a positive and negative direction according to 2 points, while in Region Crossing we detect how many people/objects flow inside and outside of a region, as well as how many people occupy the region at a given time.)

![Line + Region Crossing](/assets/line_region_crossing.png)

Loitering Detection - takes in a detection matrix and analyzes the person or object's movement over time. If the position remains within a dictated field for too long, we trigger the alarm. (Currently we don't take into account instances where a person leaves the region and then returns shortly after; this is something I would be interested in implementing in the future.)

![Loitering Detection](/assets/loitering_detection.png)

Topple Detection - takes in a detection matrix and analyzes the person or object's movement over time. If the aspect ratio and positioning rapidly changes, and remains in a prone position for a period of time, we know that a topple has occurred, and thus we trigger the alarm (which can set off a noise maker or send an email alert).

![Topple Detection](/assets/topple_detection.png)

Aggression Detection - detects physical altercations or aggressive behavior by running 2 parallel inference models, Body Pose YOLOv8 and YuNET for tracking skeletal movement and facial expressions, respectively. The node takes in this data, and evaluates movement acceleration and emotional cues to determine if a conflict is occurring.

![Topple Detection](/assets/aggression_detection.png)








