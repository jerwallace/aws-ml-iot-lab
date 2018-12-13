
# Challenge 2: Deploy an AWS Lambda Function that will perform Sentiment Analysis with AWS Rekognition

In the final section of our workshop, we will capture the sentiment from the cropped faces of concert goers in the S3 bucket.

**Step 1- Create DynamoDB table**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Dynamo

Click on Create Table.

Name of the table: recognize-emotions-your-name
Primary key: s3key

Click on Create. This will create a table in your DynamoDB.

**Step 2- Create a role for cloud lambda function**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for IAM

Choose 'Create Role'

Select “AWS Service”

Select “Lambda” and choose "Next:Permissions"

Attach the following policies: 

* AmazonDynamoDBFullAcces
* AmazonS3FullAccess
* AmazonRekognitionFullAccess
* CloudWatchFullAccess

Click Next

Provide a name for the role: rekognizeEmotions

Choose 'Create role'


**Step 3- Create a lambda function that runs in the cloud**

The inference lambda function that you deployed earlier will upload the cropped faces to your S3. On S3 upload, this new lambda function gets triggered and runs the Rekognize Emotions API by integrating with Amazon Rekognition. 

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Lambda

Click 'Create function'

Choose 'Author from scratch'

Name the function: recognize-emotion-your-name.  
Runtime: Choose Python 2.7
Role: Choose an existing role
Existing role: rekognizeEmotions

Choose Create function

Replace the default script with the script in [recognize-emotions.py](rekognize-emotions.py). You can select the script by selecting Raw in the Github page and choosing the script using ctrl+A/ cmd+A . Copy the script and paste it into the lambda function (make sure you delete the default code).

Make sure you enter the table name you created earlier in the section highlighted below:

![dynamodb](https://user-images.githubusercontent.com/11222214/38838790-b8b72116-418c-11e8-9a77-9444fc03bba6.JPG)


Next, we need to add the event that triggers this lambda function. This will be an “S3:ObjectCreated” event that happens every time a face is uploaded to the face S3 bucket. Add S3 trigger from designer section on the left. 

Configure with the following:

Bucket name: face-detection-your-name (you created this bucket earlier)
Event type- Object Created
Prefix- faces/
Filter- .jpg
Enable trigger- ON (keep the checkbox on)

Save the lambda function

Under 'Actions' tab choose **Publish**

**Step 4- View the emotions on a dashboard**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Cloudwatch

Create a dashboard called “sentiment-dashboard-your-name”

Choose Line in the widget

Under Custom Namespaces, select “string”, “Metrics with no dimensions”, and then select all metrics.

Next, set “Auto-refresh” to the smallest interval possible (1h), and change the “Period” to whatever works best for you (1 second or 5 seconds)

NOTE: These metrics will only appear once they have been sent to Cloudwatch via the Rekognition Lambda. It may take some time for them to appear after your model is deployed and running locally. If they do not appear, then there is a problem somewhere in the pipeline.

-----------------------------------
[Back (Challenge 1: Facial Detection)](../Challenge_1_Crop_Faces_With_DeepLens/README.md) | [Next (Bonus Challenge: Custom Facial Detection with SageMaker)](../Bonus_Challenge_Optional_Sagemaker/README.md)