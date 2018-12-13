# Challenge 1: Build a Project to Detect Faces and Send the Cropped Faces to S3 bucket

Now, we will crop the faces from our concert photos collected from DeepLens so we can run sentiment analysis using Rekognition. 

## Setup IAM Roles:

First, we need to add S3 permissions to the DeepLens Lambda role so the lambda on the device can call Put Object into the bucket of interest.

Go to [IAM Console](https://console.aws.amazon.com/iam/home?region=us-east-1#/home)

Choose Roles and look up AWSDeepLensGreenGrassGroupRole

Click on the role, and click Attach Policy

Search for AmazonS3FullAccess and choose the policy by checking the box and click on Attach Policy

## Create the Photos Bucket:

We need to create an S3 bucket that we can upload faces to.

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for S3

Choose 'Create bucket'

Name your bucket : face-detection-your-name

Click on Create 

## Create inference lambda function:

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Lambda

Click 'Create function'

Choose 'Blueprints'

In the search bar, type “greengrass-hello-world” and hit Enter

Choose the python blueprint and click Configure

Name the function: DeepLens-sentiment-your-name
Role: Choose an existing role
Existing Role: AWSDeepLensLambdaRole

Click Create Function

Replace the default script with the [inference script](lambdas/inference-lambda.py) . You can select the inference script, by selecting Raw in the Github page and choosing the script using ctrl+A/ cmd+A . Copy the script and paste it into the lambda function (make sure you delete the default code).

In the script, you will have to provide the name for your S3 bucket. Insert your bucket name in the code below

![code bucket](https://user-images.githubusercontent.com/11222214/38719807-b46169fa-3ea8-11e8-8ff2-69af5455ede7.jpg)

Click Save

Under the “Actions” drop-down menu, Click “Publish new version” and publish.

Note:It is important that you publish the lambda  function, else you cannot access it from DeepLens console.

## Deploy the project:

**Step 1- Create Project**

The AWS DeepLens console should open on the Projects screen, select Create new project on the top right (if you don’t see the project list view, click on the hamburger menu on the left and select Projects)

![create project](https://user-images.githubusercontent.com/11222214/38657905-82207e44-3dd7-11e8-83ef-52049e229e33.JPG)

Choose a blank template and scroll down the screen to select Next

Provide a name for your project: face-detection-your-name

Click on Add Models and choose face detection

Click on Add function and choose the lambda function you just created: Deeplens-sentiment-your-name

Click Create

**Step 2- Deploy to device**
In this step, you will deploy the Face detection project to your AWS DeepLens device.

Select the project you just created from the list by choosing the radio button


Select Deploy to device.


![choose project-edited-just picture](https://user-images.githubusercontent.com/11222214/38657988-eb9d98b6-3dd7-11e8-8c94-7273fcfa6e1b.jpg)

On the Target device screen, choose your device from the list, and select **Review.**

![target device](https://user-images.githubusercontent.com/11222214/38658011-088f81d2-3dd8-11e8-972a-9342b7b3e291.JPG)

Select Deploy.

![review deploy](https://user-images.githubusercontent.com/11222214/38658032-223db2e8-3dd8-11e8-9bdf-04779cd0e0e6.JPG)

On the AWS DeepLens console, you can track the progress of the deployment. It can take a few minutes to transfer a large model file to the device. Once the project is downloaded, you will see a success message displayed and the banner color will change from blue to green.

**Confirmation/ verification**

Congratulations! You have completed this challenge. You will now find your cropped faces uplaod to your S3 bucket!

-----------------------------------
[Back (Pre-reqs)](../PreReq_Setup_DeepLens.md) | [Next (Challenge 2: Sentiment Analysis)](../Challenge_2_Sentiment_Analysis/README.md)