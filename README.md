# Serverless-API-FRG

AMI: EC2 - t2.medium eu-west-1c <br/>

### Setup
Make sure to have an .aws credentials directory and awscli installed. <br/>

Clone the repository and navigate to its root: <br/>
`git clone https://github.com/etvincen/Serverless-API-FRG.git` <br/>
`cd Serverless-API-FRG.git` <br/>
Install required plugins: <br/>
`sls plugin install -n serverless-wsgi` <br/>
`sls plugin install -n serverless-python-requirements` <br/>
Create a new virtual environnement with virtualenv: <br/>
`virtualenv venv` <br/>
`source venv/bin/activate` <br/>
`pip install -r requirements.txt` <br/>

Modify the bucket name in code to store the JSON objects: <br/>
In app.py (at line 25), set the variable "bucket_name" to the name of one of your created bucket. <br/>

### Notes
Chosen test format: csv <br/>
Ideal test file: test_file/datagouv.csv <br/>

### Launch app and Submit a test file 
run `sls deploy` <br/>
Once the application is deployed, <br/>
run `cd test_file` <br/>
run `curl -F file=@./datagouv.csv https://ny3q4ymis8.execute-api.eu-west-1.amazonaws.com/dev/json` (The domain name delivered by the serverless app might change) <br/>

### Config deletion of uploaded ressources after 1 year
- Select the S3 bucket of your choice <br/>
- Go to Management > Life Cycle <br/>
- Click on Add a life cyle rule <br/>
- Type a name for the rule <br/>
- Tick Apply to all objects of the container <br/>
- Click next <br/>
- Leave the Transition fields blank <br/>
- Click next <br/>
- Tick Actual Version <br/>
- Tick Make the object actual versions expires <br/>
- Type 365 in the input field <br/>
- Click next <br/>
- Tick the confirmation box and click Save <br/>

The rule is now active and all objects already stored in the bucket will expire in 365 days (included).





