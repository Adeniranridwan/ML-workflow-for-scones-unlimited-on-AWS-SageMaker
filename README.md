**ML Workflow For Scones Unlimited On Amazon SageMaker**

**Problem Statement **
There is need of a Machine Learning Engineer for a scone-delivery-focused logistics company, Scones Unlimited, to ship an Image Classification model. The image classification model can help the team in a variety of ways in their operating environment such as: detecting people and vehicles in video feeds from roadways, better support routing for their engagement on social media, detecting defects in their scones, and many more!
In this project, an image classification model that can automatically detect which kind of vehicle deliavery drivers have, in order to route them to the correct loading bay and orders is developed . Assigning delivery professionals who have a bicycle to nearby orders and giving motorcyclists orders that are farther can help Scones Unlimited optimize their operations.
Data Sourcing:  The sample dataset was extracted from a hosting service into a CIFAR folder containing the meta, train and test files. The CIFAR dataset is open source and generously hosted by the University of Toronto at: https://www.cs.toronto.edu/~kriz/cifar-100-python.tar.gz

**Preprocessing**
The images extracted was explored to transform into a usable shape and format, save them as files, and capture their filenames and labels.
Since the main problem we are to solve is the detect the image of bicycle and motocycle, let's just capture all the bicycles and motorcycles and save them. Scones Unlimited can use a model that tells these apart to route delivery drivers automatically. Through exploration, we identify the label numbers for Bicycles and Motorcycles to be 8 and 48 respectively. Hence, We only need objects with label 8 and 48 -- this drastically simplifies our handling of the data! 
A new dataframe was created by safely dropping the rows that don't contain observations about bicycles and motorcycles.
This is saved in a newly created directory called train and test and eventually loaded into s3 bucket

**Model Training and deployment**
The model was built using AWS build-in image classification algorithm in Sagemaker and deployed to an endpoint. The Model Monitor was configured to track the deployment. Eventually, an inference was made to test the model endpoint.
Lambdas and step function workflow
Three Lambda functions was drafted and deployed, and the Step Functions visual editor was used to chain the lambda functions them together!
The first lambda function is responsible for data generation. The second one is responsible for image classification. And the third function is responsible for filtering out low-confidence inferences.

**Testing and evaluation**
Several step function invokations was performed using data from the test dataset. This process gives confidence that the workflow both succeeds AND fails as expected. In addition, the captured data from SageMaker Model Monitor was used to create a visualization to monitor the model.
