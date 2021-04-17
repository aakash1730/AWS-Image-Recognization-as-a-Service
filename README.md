# Image Recognition Using AWS
## Project 1 - IaaS - Amazon Web Services (CSE 546 - Cloud Computing)

## Group Members
* Aakash Patel (ASU ID: 1219522499)
* Disha Bhukte (ASU ID: 1219495225)
* Sapan Desai  (ASU ID: 1219080070)

## Details are provided in the report.

## There are two module in this project
  1 - Web-Tier
  2 - App-Tier
  
## Web-Tier-AWS
* The web tier provides a user friendly UI for the user to upload images. It then stores the image in the S3 input bucket and puts a message in the input queue for further processing. Once the image recognition is done, the webapp reads the output from the output queue and displays the result on the UI. In case of multiple requests, it automatically initiates multiple app instances for faster processing of the multiple requests. The maximum count of the app instances initiated through the web app is 19.

## App-Tier-AWS
* The app tier is used for processing the input request. Each app instance reads the message from the input queue, downloads the image from the S3 input bucket based on the key for the image present in the message of the input queue. It then recognizes the image using the provided image recognition model. The output is stored in the S3 output bucket and the input output pair is passed in the message to the output queue. When the number of requests in the input queue exceeds the maximum number of app instances created by the web tier i.e. 19, the app instance uses multithreading for handling the excess load of requests.

## Steps to install and run the code:-
* - Clone the project.
* - Import as maven project in any of the IDE(IntelliJ or Eclipse): Once the project is downloaded in the directory, import the project as a maven project in the eclipse/intellij workspace.
* - maven clean: In order to run the project, the first step is to perform maven clean.
* - maven install: The next step is to maven install on the project to download all the dependency. 
* - Change the ACCESS_ID, ACCESS_KEY as per your AWS set up in both modules(web-tier and app-tier).
* - Hit Maven-install again.
* - Create an instance from the provided AMI.
* - Use scp command to transfer the app-tier jar file to the instance created in the previous step.
* - scp -i security_key.pem /path_of_app_tier_jar ubuntu@ec2-public-dns:~ 
* - Create a new AMI after transferring the jar to an instance.
* - Copy the AMI ID created in the previous step and paste it under the AMI_ID constant in ProjectConstant.java file for the web-tier module.
* - Hit maven-install again to update the jar of web-tier.
* - Use scp command to transfer the jar file to the instance:
* - scp -i security_key.pem /path_of_web_tier_jar ubuntu@ec2-public-dns:~ 
* - login to the web-tier instance using ssh command
* - ssh -i ccproject2021.pem ec2-user@ec2-100-27-12-166.compute-1.amazonaws.com 
* - setup java environment  in the instance 
* - yum list java* 
* - sudo yum install java-1.8.0 
* - change the permissions of the jar
* - chmod +x <jarname>
* - run the web jar file
* - java -jar <path to jar file>
