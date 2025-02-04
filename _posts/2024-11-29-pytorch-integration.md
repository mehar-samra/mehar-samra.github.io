## PyTorch Integration in Infiniworkflow

After many weeks of work, Infiniworkflow is now capable of creating and deploying Machine Learning models built from scratch!

The process of integrating PyTorch began by including tools for Tensors, which are the staple datatype used by PyTorch. Tensors are similar to NumpyArrays, which is why we have many tools to convert to and from Tensors, NP Arrays, DataFlows, numerics, and even images/videos.

With this base built, I was able to begin work on Regression model training and testing, which stands as one of the simpler tasks in machine learning. This taught me how ML models work, from optimizer and criterion/loss functions to the several hidden layers that build neural nets. Each of these components can be seen in the Regression workflow below:

![Regression Workflow](/assets/ui_torch_regression.jpg)

Building the tools for Classification and Segmentation quickly followed, using preexisting datasets such as CIFAR10, MNIST, and Cityscapes built into PyTorch to perform both training and testing. An example Classification workflow can be seen below, along with how datasets appear in the Infiniworkflow UI:

![Classification Workflow](/assets/ui_cifar_workflow.jpg)

![Cifar Dataset](/assets/ui_cifar_dataset_gif.gif)

After finally achieving the implementation of ML model creation, I then had to expand the available tools to ensure they were of practical use to ML engineers, as generally speaking most engineers probably have their own unique datasets they wish to train on, not just basic ones like CIFAR or MNIST. As such, custom dataset support is now operational in Infiniworkflow, with expanded capabilities for engineers that build their own plugins.





