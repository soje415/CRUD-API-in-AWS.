# CRUD-API-in-AWS.
CRUD API with AWS API Gateway, Lambda, DynamoDB and Cloud 9 for testing



Project Description:

Your goal in this workshop is to build a very simple CRUD (Create, read, update, delete) API. To accomplish this you will be guided through a few steps. Starting with creating a DynamoDB table using the DynamoDB console, to creating a Lambda function in the AWS Lambda console. Next you will configure an HTTP API using the API Gateway console and last, after launching an AWS Cloud9 IDE you will use it to test your API!

If you have little experience with AWS but know your way around at typing commands in a terminal, this workshop is for you! (Copy/Paste allowed!)

When you invoke your HTTP API, API Gateway routes the request to your Lambda function. The Lambda function interacts with DynamoDB, and returns a response to the API Gateway. The API Gateway then returns a response to you.

Project Architecture:

![image](https://github.com/user-attachments/assets/b3935edd-73d3-41de-aae7-700fd3e04f84)


Steps to Build the Project:
Prerequisites

AWS Account with appropriate permissions to create Lambda functions, API Gateway, and S3 buckets.
Passion to Learn!


Steps to Deploy

Step 1: Create a DynamoDB table:
a. For Table name, enter: http-crud-tutorial-items
b. For Primary key, enter id![dynamodb table](https://github.com/user-attachments/assets/c1944074-02aa-4e41-b8fb-873ec046c229)




Step 2: Create a lambda function:

a. Name: http-crud-tutorial-function
b. Runtime: Python 3.x
c. Execution role: IAM role with DynamoDB and API permissions
d. Code: Use the CURD.py Python code from the file above
![lambda](https://github.com/user-attachments/assets/e926bc3d-0098-4103-8032-63308bd601a1)



Step 3: Create an HTTP API in API Gateway

Name: http-crud-tutorial-api
![APIGATEWAY](https://github.com/user-attachments/assets/a4be347c-f533-4d22-bfbd-8582844d6e8e)



Step 4: Create routes: \


GET /items/{id}

GET /items

PUT /items

DELETE /items/{id}
![route get,put,delete](https://github.com/user-attachments/assets/37d555cf-aae1-49f2-a45d-7af416c8fbf7)


Step 5: Create an integration: \


a. Choose your API (http-crud-tutorial-api)
b. Choose Integrations
c. Choose Manage integrations and then choose Create Skip Attach this integration to a route. You complete that in a later step.
d. For Integration type, choose Lambda function
e. For Lambda function, enter http-crud-tutorial-function \

All intergrations are attached to the Lambda function
![intergration attachment](https://github.com/user-attachments/assets/9a592419-bf80-4c66-ac0f-17f191db63e6)



Step 6: Attach your integration to routes:

a. Choose your API (http-crud-tutorial-api)
b. Choose Integrations
c. Choose a route
d. Under Choose an existing integration, choose http-crud-tutorial-function
e. Choose Attach integration
f. Repeat steps 4-6 for all routes. All routes show that an AWS Lambda integration is attached.
g. Note your API's invoke URL. It appears under Invoke URL on the Details page.


Step 7: Create Cloud9 Environment


Step 8: Testing:


Export API Invoke URL: \
export INVOKE_URL="https://**abcdef123**.execute-api.eu-west-1.amazonaws.com"
![invoke url](https://github.com/user-attachments/assets/b6f39d01-4a81-4d1c-8ca2-c98dbfb574f5)


Create or update an item. 

The command includes a request body with the item's ID, price, and name. \
curl -X "PUT" -H "Content-Type: application/json" -d "{
  \"id\": \"abcdef234\",
  \"price\": 12345,
  \"name\": \"myitem\"
}" $INVOKE_URL/items

![use](https://github.com/user-attachments/assets/de8278ac-fba4-494e-8b17-4ae985bd7ef3)

Further verification from the item create in the dynamoDB table we created earlier. 
We have succeesfully PUT 
![items added](https://github.com/user-attachments/assets/8a2fcf03-0490-4199-9bbd-e17003740ea5)




Use the following command to list all items.

curl -s $INVOKE_URL/items | js-beautify 


Use the following command to get an item by its ID.
curl -s $INVOKE_URL/items/abcdef234 | js-beautify


Use the following command to delete an item.
curl -X "DELETE" $INVOKE_URL/items/abcdef234


Use the following command to list all items.
curl -s $INVOKE_URL/items | js-beautify 
