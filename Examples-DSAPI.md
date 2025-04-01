# Some examples on using DataStage API

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
DataStage API services link - https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/ds-apis.html?audience=wdp&context=cpdaas \

This is the command to assign access token to the ${ACCESS_TOKEN} variables.
```
export ACCESS_TOKEN=$(curl -H "Content-Type: application/x-www-form-urlencoded" -X POST -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=${IBMCLOUD_APIKEY}" --url "https://iam.cloud.ibm.com/identity/token" | jq -r '.access_token')
```

When you run this to load the variables, the above are automatically handled.
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

To get jobs from Project based on project id.
```
curl -X 'GET' \
  "https://api.au-syd.dai.cloud.ibm.com/v2/jobs?project_id=${PROJECT_PROD}&limit=100&userfs=false" \
  -H 'accept: application/json' \
  -H "Authorization: Bearer ${ACCESS_TOKEN}"
```
![image](https://github.com/user-attachments/assets/9b4d9c33-5a10-4473-9aee-01990173a15b)


To get information of jobs based on project and job ids.










