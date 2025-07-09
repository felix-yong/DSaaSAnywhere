# Some examples on using command line `cpdctl`

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
Command reference can be find in this link - https://github.com/IBM/DataStage/blob/main/dsjob/Readme.md \
Install and configure `cptctl` tool is available in this link - https://github.com/IBM/cpdctl/blob/master/README.md \
Example used here is based on 5.1.1 and the Data Center Information are below -
- Dallas: dataplatform.cloud.ibm.com and api.dataplatform.cloud.ibm.com
- Frankfurt: eu-de.dataplatform.cloud.ibm.com and api.dataplatform.cloud.ibm.com
- Sydney: au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com
- Toronto: ca-tor.dai.cloud.ibm.com and api.ca-tor.dai.cloud.ibm.com

## _In the examples, I did use hardcode info like ProjectID, JobID, etc which is based on my environment. Please make sure you change it to cater for your environment._

### When you run this to load the variables, it will run the setup profile below
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

### Setup the cpdctl to run DataStage in those example
***To enable dsjob in cpdctl. You can add this to .bash_profile so that it will be loaded whenever you login***
```
export CPDCTL_ENABLE_DSJOB=true
```

***Setup the cpdctl profile using profile name `dsaas` based on Sydney Data Center. Data Center Information***
```
cpdctl config profile set dsaas --url ${DSJOB_URL} --apikey ${IBMCLOUD_APIKEY} --watson-studio-url https://api.au-syd.dai.cloud.ibm.com
```

***To use certain profile as the current profile, for example to use the profile create above***
```
cpdctl config profile use dsaas
```

`A status code is printed to the output. A status code of 0 indicates successful completion of the command.`

### Example 01, this command list all projects.
```
cpdctl dsjob list-projects
```
![image](https://github.com/user-attachments/assets/4549be43-2f84-42dc-b8de-73acfe6485cc)

### Example 02, this command show all the environment information of the project.
```
cpdctl environment list --project-id ${PROJECT_PROD}
```
![image](https://github.com/user-attachments/assets/a2712fcd-4201-4936-980b-a4f1e60401dd)


### Example 03, this command list all jobs in the project based on project id and sorted it alphabetically.
```
cpdctl dsjob list-jobs --project-id ${PROJECT_PROD} --sort
```
![image](https://github.com/user-attachments/assets/9a224cc8-78b8-4a20-b000-4c060f203803)

### Example 04, this command list all jobs in the project based on project id, sorted it alphabetically and with job-id.
```
cpdctl dsjob list-jobs --project-id ${PROJECT_PROD} --sort --with-id
```
![image](https://github.com/user-attachments/assets/14118ffb-ceb5-4ea2-b554-176c62308915)

### Example 05, this command list all jobs in the project based on project name and sorted it alphabetically.
```
cpdctl dsjob list-jobs --project "DSaaSAnywhere" --sort
```
![image](https://github.com/user-attachments/assets/c368f511-1771-470a-8a57-317de85db38d)


### Example 06, this command get information about job using project id and job id.
```
cpdctl dsjob get-job --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e
```
![image](https://github.com/user-attachments/assets/73e55669-32e9-42ba-bee0-e50fc048c4d9)

### Example 07, this command get information about job using project id and job name.
```
cpdctl dsjob get-job --project-id ${PROJECT_PROD} --name "DSFlow.DataStage job"
```
![image](https://github.com/user-attachments/assets/d63ec230-49e7-4964-ba37-f0396f0bb3a1)

### Example 08, this command list the status of the job using project id and job id for the last job run.
```
cpdctl dsjob list-job-status --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e
```
![image](https://github.com/user-attachments/assets/69eb574a-6f2c-426f-a54a-b7a8df603230)

### Example 09, this command list the status of the job using project id and job id for all job run with sort.
```
cpdctl dsjob list-job-status --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e --sort --with-past-runs
```
![image](https://github.com/user-attachments/assets/30964d64-0acc-4537-abf0-50142b53bb13)

### Example 10, this command provide basic job information using project id and job id.
```
cpdctl dsjob jobinfo --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e
```
![image](https://github.com/user-attachments/assets/dfd3a5b7-8e36-4429-82d2-f813f4f693c2)

### Example 11, this command provide full job information using project id and job id.
```
cpdctl dsjob jobinfo --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e --full
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/3eadfe8f-ad44-41e1-b9c4-8dfe077d4b70)

### Example 12, this command project basic job information and parameters using project id and job id
```
cpdctl dsjob jobinfo --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e --list-params
```
![image](https://github.com/user-attachments/assets/7decf01d-6cf2-45cd-97ea-b972632feff9)

### Example 13, this command provide the most comprehensive job information and parameters using project id and job id.
```
cpdctl dsjob jobinfo --project-id ${PROJECT_PROD} --id 0ce41049-b7a0-4073-8aa5-50dc8790da4e --full --list-params
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/d637b3ef-41eb-4f51-98c5-aa27cc095397)

### Example 14, this command will run a job based on project id, job id and using default engine. The setting of wait -1 will wait for the job to finish.
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --wait -1
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/5c50c8f6-8ca4-4ac0-87bd-478373868415)
![image](https://github.com/user-attachments/assets/784621f9-1df7-4a5e-a4b0-9dc82f18a6c1)

### Example 15, this command will run a job based on project id, job id and using engine specifed. The setting of wait -1 will wait for the job to finish.
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --id 53df39c5-45e5-410a-9686-a7beaeaa6d34 --runtime-env datastage-ocp02 --wait -1
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/5d028bbe-58c6-4fee-ad29-8e67a37cb3c1)
![image](https://github.com/user-attachments/assets/cbb24ac9-2132-4540-bd1b-24fceb53a84c)

### Example 16, this command will run a job based on project id, job id and using default engine. The setting of wait -1 will wait for the job to finish and passing in a local parameter value.
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --param RowsGen=10000000 --wait -1
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/0e347dde-636d-4c3e-bfdc-515d8d8c794d)
![image](https://github.com/user-attachments/assets/f0c16dfe-ca06-4607-a4d3-9c714ea18e4a)

### Example 17, the DataStage NextGen support multi-instance jobs without requirements to enable it. In this example, I will show how it work.
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --param RowsGen=1000000000
```
***Issue the same command again to run the same job with a unique runtime env value.***
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --param RowsGen=1000000000
```
![image](https://github.com/user-attachments/assets/3151b2e8-9969-48b5-b6d2-1f136edd8d9d)
![image](https://github.com/user-attachments/assets/15e2d704-4c81-405f-926f-8b67c573b370)
![image](https://github.com/user-attachments/assets/5c803d6f-6375-4c05-9bc0-5ca43772c916)
![image](https://github.com/user-attachments/assets/0a3427c7-100a-4d83-97aa-35284f300d4e)

### Example 18, this is another example of running multi-instance of the same job but using 2 difference engine
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --job-id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --param RowsGen=1000000000
```
***Issue the same command again to run the same job with a difference engine name in runtime env value***
```
cpdctl dsjob run --project-id ${PROJECT_PROD} --job-id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --param RowsGen=1000000000 --runtime-env remote_engine_ibmcloud_SYD-SYD11
```
![image](https://github.com/user-attachments/assets/ddf160f9-3f26-4983-9ba5-d3a5f755ff90)
![image](https://github.com/user-attachments/assets/2bcc511d-4a21-4a09-a7a9-b037f5f087a9)
![image](https://github.com/user-attachments/assets/bb87a6d7-499c-447c-88fa-d40d6dba763c)
![image](https://github.com/user-attachments/assets/cc0176f7-903b-4e52-b67f-18c6fdf144c5)

### Example 19, this command will provide the job status when you didn't use the wait -1
```
cpdctl dsjob waitforjob --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --run-id 45deb910-8ff5-4465-9848-8ca4ca189d1a
```
![image](https://github.com/user-attachments/assets/8185b7f4-0642-4fd3-aedc-455c68dd522c)

### Example 20, this command will provide the job logs information.
```
cpdctl dsjob logdetail --project-id ${PROJECT_PROD} --id 0327d1a3-a2a1-46a4-9087-862ee34cd239 --run-id 45deb910-8ff5-4465-9848-8ca4ca189d1a
```
***The screenshot didn't managed to capture all information provided.***
![image](https://github.com/user-attachments/assets/58cc7142-ea4a-4b6a-8876-0bef216ffb73)
![image](https://github.com/user-attachments/assets/b7b8f3b9-ccb1-418d-9f62-72271d03a32c)

### Example 21, this command will list all the DataStage runtime environment information for the specified project.
```
cpdctl dsjob list-envs --project-id ${PROJECT_PROD} --types datastage --full --sort --with-id
```
![image](https://github.com/user-attachments/assets/d426a0e0-a03b-4156-bf78-affc217afc5a)

### Example 22, this command get the specified DataStage runtime environment information for the specified project.
```
cpdctl dsjob get-env --project-id ${PROJECT_PROD} --id 9277bc28-b898-4a4e-9e24-da02e6123582 --output json --with-metadata
```
![image](https://github.com/user-attachments/assets/9b3a9065-5f41-4f4c-b315-32a7a87e4535)

### Example 23, this command generate a file for the specified DataStage runtime environment information for the specified project.
```
cpdctl dsjob get-env --project-id ${PROJECT_PROD} --id 9277bc28-b898-4a4e-9e24-da02e6123582 --output file  --file-name datastage-ocp02.json --with-metadata
```
![image](https://github.com/user-attachments/assets/0597028a-8e2b-4ac2-8f8c-80d9011a13c4)

### Example 24, this command leverage the file generated from Example 22 to create a DataStage runtime environment in another project.
```
cpdctl dsjob create-env --project-id ${PROJECT_DEV} --file-name datastage-ocp02.json
```

