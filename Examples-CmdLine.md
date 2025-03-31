# Some examples on command line `cpdctl`

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
Command reference can be find in this link - https://github.com/IBM/DataStage/blob/main/dsjob/Readme.md \
Example used here is based on 5.1.1 and the Data Center Information are below -
- Dallas: dataplatform.cloud.ibm.com and api.dataplatform.cloud.ibm.com
- Frankfurt: eu-de.dataplatform.cloud.ibm.com and api.dataplatform.cloud.ibm.com
- Sydney: au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com
- Toronto: ca-tor.dai.cloud.ibm.com and api.ca-tor.dai.cloud.ibm.com

Setup the line profile using profile name `dsaas` based on Sydney Data Center. Data Center Information
```
cpdctl config profile set dsaas --url ${DSJOB_URL} --apikey ${IBMCLOUD_APIKEY} --watson-studio-url https://api.au-syd.dai.cloud.ibm.com
```

`A status code is printed to the output. A status code of 0 indicates successful completion of the command.`

This command list all projects in the DSaaS instance that you connect to.
```
cpdctl dsjob list-project
```
![image](https://github.com/user-attachments/assets/4549be43-2f84-42dc-b8de-73acfe6485cc)

This command list all jobs in the project based on project id and sorted it alphabetically.
```
cpdctl dsjob list-jobs --project-id ${PROJECT_PROD} --sort
```
![image](https://github.com/user-attachments/assets/9a224cc8-78b8-4a20-b000-4c060f203803)

This command list all jobs in the project based on project id, sorted it alphabetically and with job-id.
```
cpdctl dsjob list-jobs --project-id ${PROJECT_PROD} --sort --with-id
```
![image](https://github.com/user-attachments/assets/14118ffb-ceb5-4ea2-b554-176c62308915)

This command list all jobs in the project based on project name and sorted it alphabetically.
```
cpdctl dsjob list-jobs --project "DSaaS Anywhere" --sort
```
![image](https://github.com/user-attachments/assets/c368f511-1771-470a-8a57-317de85db38d)


This command get information about job using job id.
```
cpdctl dsjob get-job --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e
```
![image](https://github.com/user-attachments/assets/73e55669-32e9-42ba-bee0-e50fc048c4d9)

This command get information about job using job name.
```
cpdctl dsjob get-job --project-id ${PROJECT_PROD} --name "DSFlow.DataStage job"
```
![image](https://github.com/user-attachments/assets/d63ec230-49e7-4964-ba37-f0396f0bb3a1)










