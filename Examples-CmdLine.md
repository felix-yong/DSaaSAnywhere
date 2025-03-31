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

