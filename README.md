# DataPalooza: A Music Festival themed ML + IoT Workshop

Welcome to DataPalooza! 

Your bold startup has taken the challenge of providing a new type of EDM music festival experience. At venues with multiple stages, festival-goers are always looking to identify which DJ stage areas are the liveliest. This causes them to constantly move around between different stages and miss out. You are looking to use Machine Learning and IoT to come up with a connected fan experience that takes the music festival scene to the next level. From your initial research there are existing ML models that you can leverage to do face and emotion detection, but there are two ways that the predictions (inference) can be done; on the cloud and on the camera itself, but which one will work the best for your needs at the festival? 

You are going to learn about both approaches and find out! 

In this workshop you will use AWS and Intel technologies including Amazon SageMaker with Intel C5 Instances, AWS DeepLens, AWS Greengrass, Amazon Rekognition, AWS Lambda

The objective of the workshop is to learn how to build and deploy a machine learning model and then run inference on it from the cloud and from the edge device.

By the time you’re done with these challenges, EDM DJ’s will be able to tell whether the crowd is enjoying their set by the looks on their faces!

Here is what you will learn today:

1. How to setup and connect to an AWS Deep Lens device.
2. How to modify the DeepLens inference lambda function to upload cropped faces to S3
3. How to deploy the inference lambda function and face detection model to AWS DeepLens
4. How to create a lambda function to trigger Rekognition to identify emotions
5. How to create an AWS DynamoDB table to store the recognized emotions
6. How to analyze data using Amazon CloudWatch
**Bonus:** How to build and train a face detection model in SageMaker

### **Pre-req:** Register and Configure your DeepLens device
*Note: You will need an active AWS account to get started. To create one, [click here](https://portal.aws.amazon.com/billing/signup?redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start).*

Before we get going, take a moment to setup and register your Deep Lens. After you have finished registering the device, run a simple Hello World application that detects faces using the default and included ML models for Deep Lens. 

**[>> Click here to Complete Pre-reqs!](Part_1_Setup_DeepLens.md)**

### **Challenge 1:** Deploy an AWS Lambda Function and Detection Model to Detect and Crop Faces from a Video Feed

The first stop in the pipeline of your Crowd Emotion Tracking App is a face-detection model. You will be using Rekognition to detect face emotions. Rather than sending a stream of raw images to Rekognition, you are going to pre-process images with the face-detection model to:
* Only send images to Rekognition when a face is detected
* Only send the actual face crop itself

This limits both the number of API calls you make, as well as the size of content you send.

In this challenge, you will use the built in face-detection model with AWS DeepLens and an AWS lambda function to crop and upload only the faces that are detected to S3.

**[>> Click here to Start Challenge!](Prep_Challenge/README.md)**

### **Challenge 2:** Deploy an AWS Lambda Function that will perform Sentiment Analysis with AWS Rekognition

The next step of the pipeline will be to analyze the photos that are being written into the S3 bucket. To recap, our goal is to find out if our concert goers are having a good time and enjoying our set. In this challenge, we will deploy a lambda function that uses the AWS Rekognition APIs to process the images of cropped faces and writes the results to a DynamoDB table and a set of metrics to a CloudWatch dashboard.  

**[>> Click here to Start Challenge!](Part_3_Sentiment_Analysis.md)**

### **Bonus Challenge:** Deploy Your Own Facial Detection Model using Amazon Sagemaker

Hey wizards! If you have zipped through the lab, try building your own facial detection model using Amazon Sagemaker. For other labs and fun activities with the Deep Lens, check out this repository. 

**[>> Click here to Start the Bonus Challenge!](Part_4_Optional_Sagemaker/README.md)**

## [Closeout](closeout.md)

During this event you have created quite a few resources, this section will cover deleting things so you do not end up with a surprise bill.