# Splunk-integrated-with-Amazon-Web-Service-AWS-
### Introduction
In today's cloud-driven world, organizations rely on powerful tools like Splunk to gain visibility into their infrastructure and security posture. This lab walks through the process of integrating Splunk with Amazon Web Services (AWS) to collect and analyze cloud storage data. You'll go hands-on with setting up a Splunk environment, configuring AWS S3 buckets, and using access credentials to securely transfer and visualize data. By learning how these systems work together, you gain critical insight into real-world log management and cloud monitoring practices.

### Objectives
- By the end of this lab, you will be able to:
- Log in to and configure Splunk for data collection.
- Create and manage an S3 bucket in AWS to store structured data.
- Generate and use AWS Access Keys for secure integration.
- Install and configure the AWS Add-on for Splunk.
- Set up custom data inputs from AWS to Splunk.
- Upload sample data (CSV files) to S3 and verify data ingestion into Splunk.
- Perform a basic search in Splunk to confirm successful data onboarding from AWS.
  
## LAB 1

### Step 1. Log in to Splunk 
- Go to splunk.com and log in
- Click on Products
- Free trials and Downloads
- Universal Forwarder
- click Download under `64 Bit Windows 10, 11, Server, 2022`

### Step 2. Create an Instance in the AWS S3 Buckets
Note: Authentication (AWS Access key / Secret key) Splunk needs `AWS Authentication key` to access `AWS logs/data`, so we have to enable some services in `AWS`.
- - Create `S3 Buckets`
  - Go to AWS console and log in
  - Under search type S3
  - Click on S3 (Scalable storage in the cloud)
  - Click create Bucket
  - -  Fill out the Following:
    -  Name: `kylebucket7958`
    -  Object Ownership: Default (ACLs Disabled)
    -  Block Public Access: uncheck `block all access` and check `I Acknowledge ...`
    -  Note: Leave the remaining of the setting and under the Bucket key check `Disable` and Scroll down and click `Create Bucket`.

  ![image](https://github.com/user-attachments/assets/b113048d-9375-41d4-b271-74ceda270859)
  ![image](https://github.com/user-attachments/assets/bde2ba9e-eddb-4944-9787-a875ec897ce5)
  ![image](https://github.com/user-attachments/assets/fcb8f831-67d5-422e-8510-630931a46cba)
  ![image](https://github.com/user-attachments/assets/7034d2cf-3919-4d98-9c43-f881b3464782)
  ![image](https://github.com/user-attachments/assets/8608b111-880c-4f7e-9fb4-a8532c4724b4)
  ![image](https://github.com/user-attachments/assets/0608f7d9-2eb3-469f-8641-4e8d2270340c)
    
 ### Step 3. Create Access and Secret Keys in AWS
 - Click on the `account name` in the top right corner
 - Go to `Security and Credentials`
 - Scroll down to Access Key and click on `Create Access Key` NOTE: If you already have one, use that `Key ID` and `Secret KEY`, but if no,t proceed to this process
 - Check `other`, click on Next
 - Leave `Description tag` Click `Create Access Key`
 - Copy both Key ID and Secret Key and save them `in Notepad` because we will need them later.
 - Download the CSV File and save.

   ![image](https://github.com/user-attachments/assets/cc685bf6-ca45-46b7-92d0-4537b6aa06bb)
   ![image](https://github.com/user-attachments/assets/60d944a3-e48b-4ac2-9a9e-79f58c8c6123)
   ![image](https://github.com/user-attachments/assets/fb5604d2-8fb0-4d08-af08-e1ed85e23569)
   ![image](https://github.com/user-attachments/assets/781ede16-0c35-4f94-ad44-5a59c3a77056)
   ![image](https://github.com/user-attachments/assets/58bbaede-ed7e-46a8-ba63-50707102cf2b)

### Step 4. Log in to Splunk
- Create a new `index` to capture data in Splunk (Refer to `Part 6` `Step 2` and Name it :`AWScap`)
- Go to `Apps`, click on `Find More Apps`, Search `aws`, click on `Install Aws Add-on on Spluck` to install, Click `Open App`.
- Under Login and Install. Use your Splunk log in credentials to log in, `Username` and `Password` then click `Agree` and Install
- After installing click on `Open the App`.

![image](https://github.com/user-attachments/assets/6492e1ba-fc08-400d-87e1-823e43ae3308)
![image](https://github.com/user-attachments/assets/d35d30ae-eaea-4a74-b37c-ea9ef4cf24de)
![image](https://github.com/user-attachments/assets/ad0f5227-2566-48f1-b9b5-f99879b3517e)
![image](https://github.com/user-attachments/assets/715a5885-a781-4c35-8ef2-68fb2d21359e)
![image](https://github.com/user-attachments/assets/d8928607-c8fc-459a-bd9a-233a05f15fd0)
![image](https://github.com/user-attachments/assets/c1f64c1d-a5e3-48fb-bfec-e79b11f98a20)


### Step 5. Add Account with AWS Credentials. That's the (Access Key)
- Click on `Configuration`.
- Click on `Add` (Make sure you are in the `Account tab`)
- - Name: `AWSaccount`
  - Key ID : `AKIA4SZHNXLLHWZYK478`
  - Secret Key: `Sbs3XaNsWr++r99mn4tb159yTHHCRZbnYZ8EIDDc`
  - Region `Globa` and click `ADD`.

![image](https://github.com/user-attachments/assets/4df395eb-23f1-4c3b-ba9d-811a301a67c6)
![image](https://github.com/user-attachments/assets/92a8161b-0e77-4b33-9dc7-c3f789a34647)
![image](https://github.com/user-attachments/assets/611aea19-c190-44c7-b06f-a10c9069f839)
![image](https://github.com/user-attachments/assets/50d72ffa-b407-47b8-bd77-92faa5c59ce4)
![image](https://github.com/user-attachments/assets/d051280a-840b-4c30-b570-aa817a9ddee7)

### Step 6. Create New Inputs
- Click on `Inputs`
- `Custom Data Type`
- Generic S3 and fill out the Forms
- - AWS Name: `S3dataonboarding`
  - AWS Account: 'AWSaccount`
  - Leave, `Assume Role/Region/Use Private Endpoint`
  - S3 Bucket: `klyebucket7958`
  - Leave `Key Prefix`
  - Start Date/Time: `2024 Back date the Date`
  - End Date/Time:
  - Source Type: AWS:`S3`
  - Index: `AWScap` and Click on `ADD` to Add

![image](https://github.com/user-attachments/assets/939fb1ce-f89c-4300-aa1d-eaddf74526aa)
![image](https://github.com/user-attachments/assets/0542c2a6-183f-436a-8bf2-4c7430417003)
![image](https://github.com/user-attachments/assets/40527c30-54f7-4192-815d-83d0954c98ee)
![image](https://github.com/user-attachments/assets/b58104c6-19b8-4796-8f0d-9480a3a09fff)


### Step 7. Upload Any CSV File an S3 Bucket
- Open the `S3 bucket` in a different Browser
- Locate your S3 name: `kylebucket7958` Click on the name
- Click `Upload`
- Click `add file`
- Locate our CSV file used from the beginning of this Lab, select Add, and click on `Upload`
- - Note: Now Splunk will go to AWS and ask for data from the S3 Bucket because we created an input around that Splunk will ask AWS to share that data with.
  - So AWS will request an authentication key before allowing Spluck to access the data.
  - Then Spluck will give the Authentication key, which was provided in the cost of creating the account
  - And then Spluck will log into AWS to fetch the requested data 

![image](https://github.com/user-attachments/assets/ee988bd3-0a35-469f-b4ce-bf55cee97dea)
![image](https://github.com/user-attachments/assets/2f29119c-ea91-419f-a95c-9e8bcfd8af9c)
![image](https://github.com/user-attachments/assets/82ae1e5d-bbd1-45a2-a06f-1382e8b44b70)
![image](https://github.com/user-attachments/assets/6a079aa7-b10f-4f83-8f28-e2dbccffa3ba)
![image](https://github.com/user-attachments/assets/f5e0a7ce-8666-440d-882e-f9f9cf486a3c)
![image](https://github.com/user-attachments/assets/1140b5d4-5405-47d5-98ba-d83d37a4c476)

### 8. Verify if the inputs have been created
- Go to `Apps` in Splunk
- Click on `Search/reporting`
- - Type: `indes=awscap` press enter
  - Click on Host: You will see the `host IP` under Values
  - Click on Source: Under Value, you will see `S3://kylebucket7958/csvfile`
  - Click on Source Type: you will see `AWS: S3`

![image](https://github.com/user-attachments/assets/9f745854-f0b3-4501-b531-76a024a80c59)
![image](https://github.com/user-attachments/assets/e82f7082-d71c-4a46-9a34-14f46078e52f)
![image](https://github.com/user-attachments/assets/c60c8416-bc2a-4fe2-9abc-834af35870f3)
![image](https://github.com/user-attachments/assets/cc6eab70-e36e-4ca5-80c4-db0cb00212d8)
![image](https://github.com/user-attachments/assets/26bb9ec2-bfc4-420a-a7a7-e33f478fa4e8)
