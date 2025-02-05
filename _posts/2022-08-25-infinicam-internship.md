## Photron Summer Internship 2022

For my first internship with Photron, I was tasked with creating new programs and testing the existing ones that would accompany the Infinicam (Photron's newest high-speed camera) when it launched officially later that year.

I developed 3 projects during my first month of the internship. The first was a rudimentary program for sending high speed camera data across the Internet via a websocket server; the image data from the camera was vectorized, and that vector data was what was sent across the websocket. The second project displayed feed from the Infinicam onto GameObjects in Unity, with the GameObjects being fully interactable objects. 

However, as development was being done on the third project, CVTiles, it was decided that this would be the most interesting project of the three I created to launch with Infinicam. The goal of CVTiles was to use the Infinicam to create high-definition scans for rapidly moving objects. In order to keep up with the extremely high frame rate (roughly 30,000 FPS), a very high performance system design was necessary from the beginning, which is why CVTiles utilizes Multi Threading. While the UI thread runs in 60 FPS to draw the user interface and handle keyboard/mouse events, the Capture thread could continue at 30K FPS to capture image data in a ring buffer.

A link to the presentation can be found here: [END OF INTERNSHIP 2022 SLIDES](https://docs.google.com/presentation/d/1pPLoXk22V4BJVRg7-sZlmW9AaLYE0ug7jCiTrTpFBPg/edit?usp=sharing)


