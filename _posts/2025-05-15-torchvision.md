## PyTorch Torchvision Models in Infiniworkflow

Torchvision is a package within PyTorch that provides resources for computer vision tasks, including large pre-trained models for image detection, segmentation, and more. Having built the system of creating Neural Network models from scratch in Infiniworkflow, it seemed like a logical next step to integrate pre-trained models. Now, we have a few dozen models ready, from Resnet and Alexnet to VGG and InceptionV3.


However, there is a level between using pre-trained models and making models entirely from scratch, which is to adapt pre-trained models to specific datasets -- something we can accomplish with feature learning and fine tuning. 

![Fine Tuning and Feature Extraction](/assets/finetuning_and_featureextraction.png)


Fine tuning works by taking the pre-trained model's paramaters and using them for further training on the target dataset. Feature learning on the other hand uses what the pre-trained model learned to extract meaningful features for new data or to accomplish a specific task.

Perhaps the most difficult part of implementing these trainable models was  adapting code written by engineers in Tokyo using Mask2Former, a model for performing segmentation, as it was very long and mostly written in Japanese. However, once I got the code working for the Mask2Former node, I was then able to break the Mask2Former node code into its base components so that I could add fine tuning capabilities. This means we can add custom parameter values and train up the custom Mask2Former model on our data, as seen below.

![Mask2Former Fine Tuning](/assets/mask2former.png)






