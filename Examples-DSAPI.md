# Some examples on using DataStage API

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
DataStage API services link - https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/ds-apis.html?audience=wdp&context=cpdaas \

### This is the command to assign access token to the ${ACCESS_TOKEN} variables.
```
export ACCESS_TOKEN=$(curl -H "Content-Type: application/x-www-form-urlencoded" -X POST -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=${IBMCLOUD_APIKEY}" --url "https://iam.cloud.ibm.com/identity/token" | jq -r '.access_token')
```

### When you run this to load the variables, the above are automatically handled.
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

### Example 01, to get jobs from Project based on project id.
```
curl -X 'GET' \
  "https://api.au-syd.dai.cloud.ibm.com/v2/jobs?project_id=${PROJECT_PROD}&limit=100&userfs=false" \
  -H 'accept: application/json' \
  -H "Authorization: Bearer ${ACCESS_TOKEN}"
```
![image](https://github.com/user-attachments/assets/9b4d9c33-5a10-4473-9aee-01990173a15b)

### Example 02, to get information of job based on project and job ids.
```
curl -X 'GET' \
  "https://api.au-syd.dai.cloud.ibm.com/v2/jobs/0327d1a3-a2a1-46a4-9087-862ee34cd239?project_id=${PROJECT_PROD}&userfs=false" \
  -H 'accept: application/json' \
  -H "Authorization: Bearer ${ACCESS_TOKEN}"
```
![image](https://github.com/user-attachments/assets/3fa97719-4458-41e5-89e0-c8bdf3f3f2fe)

### Example 03, to get job run information of job based on project and job ids.
```
curl -X 'GET' \
  "https://api.au-syd.dai.cloud.ibm.com/v2/jobs/0327d1a3-a2a1-46a4-9087-862ee34cd239/runs?project_id=${PROJECT_PROD}&limit=100&userfs=false" \
  -H 'accept: application/json' \
  -H "Authorization: Bearer ${ACCESS_TOKEN}"
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/ad150dfa-a994-4fc9-8fb8-1c7da69bb44a)
![image](https://github.com/user-attachments/assets/c8f251f5-c76a-4420-a164-9ce50076f5d8)







