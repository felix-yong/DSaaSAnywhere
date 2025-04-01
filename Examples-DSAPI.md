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














