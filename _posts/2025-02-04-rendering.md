## 3D Rendering in Infiniworkflow

The most recent major update to Infiniworkflow is the addition of 3D Rendering capabilities, which utilizes PyRender and Matplotlib to construct and render 3D scenes.

After reading through the PyRender documentation files, we determined the best approach to integrating PyRender into Infiniworkflow, which was to have all Mesh and Lighting nodes produce 3DNodes as the output type. These then could be combined into parent Nodes (also with 3DNode as the output type), or could be brought in directly to a Render Scene node. The capability to add multiple inputs in designated Infiniworkflow nodes allows user flexibility in determining how they want their scene to be constructed. A Camera and Camera Control Matrix can be brought in as inputs (whether the Camera be a Perspective Cam, Orthogonal Cam, or Intrinsic Cam), but they are not required to visualize the scene thanks to our default Camera controls built into the Render Scene node.

The main intent behind bringing 3D Rendering into Infiniworkflow, besides applications for Computer Graphics engineers, is to allow for easy creation of data for segmentation training. In order to perform Segmentation (a key task for self-driving cars, robots, and much more), the ML model responsible for Segmentation needs to have a large dataset wherein all important objects in each image of the dataset are segmented or broken down (i.e. we need a highlighted region for each car, person, and road in an image for a self-driving car). This is a tedious task to attempt to do by hand, as a human needs to go in a highlight each distinct region of the image. However, with a 3D Renderer, all segmentation can be done instantly, as the 3D Renderer has access to all objects in the scene and their positional data; therefore, if you wanted to highlight all cars in a 3D Rendered Scene, that could be done automatically by selecting all objects that represent a car.

As such, having PyRender in Infiniworkflow means the process of creating, training, and deploying custom ML models for Segmentation is now easier than ever.


