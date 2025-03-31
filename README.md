# DSaaSAnywhere

This is a documentation related to DataStage as a Service Anywhere

# Information / Reference

Supported Kubernetes (K8s) Services (See this link for latest update) – (Info below is as of 20250328) \
•	OpenShift \
•	IBM K8s Services (IKS) \
•	Amazon Elastic K8s Services (EKS) \

Supported OS (See this link for latest update) for docker/podman– (Info below is as of 20250328) \
•	Red Hat Enterprise Linux (RHEL) 8.8, 8.10, 9.2 and 9.4 \
•	Ubuntu 20.04, 22.04, 24.04 \

URL for SYD Data Center of CPDaaS/DSaaS – au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com

DSaaS Anywhere LI – https://www.ibm.com/support/customer/csol/terms/?id=i126-9243&lc=en

SLA for IBM Cloud (See this link for latest update) – DSaaS is Tier 3 at 99.99% (Info is as of 20250328). The following are some pointers to read the link. \
•	See Section 4 for the SLAs availability. \
•	See Section 6 for the Supported SLA Tiers by service. DataStage is at pg 11 of 19. \

Documentation link to DSaaS – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/datastage.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS Anywhere remote engine – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/create-remote-engine.html?context=cpdaas&audience=wdp \
•	Direct link for Docker – https://github.com/IBM/DataStage/tree/main/RemoteEngine/docker \
•	Direct link for K8s – https://github.com/IBM/DataStage/tree/main/RemoteEngine/kubernetes \
Documentation link to FAQ for DSaaS Anywhere – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/remote_engine_faqs.html?context=cpdaas&audience=wdp \
Documentation link to security for DSaaS Anywhere remote engines – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/security_for_remote_runetime_engines.html?context=cpdaas&audience=wdp \
Documentation link on sharing the remote engines across projects – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/sharing_remote_engine.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS command-line tools – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/cli.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS APIs – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/ds-apis.html?context=cpdaas&audience=wdp

# Questions and Answers

How to find the ProjectID? \
You can find it on the URL from the UI as highlighted in the screenshot below \
![image](https://github.com/user-attachments/assets/41449638-b79b-4873-b4d3-db6fd991f765) \
You can find it within the Project you click on -> Manage -> General in the screenshot below. In my example, I click on a project name DSaaS Anywhere. \
![image](https://github.com/user-attachments/assets/1cdf7552-9fe6-45fb-b7bd-44a6b6d83991)

Why we need persistent volumes for containers? \
Persistent volumes are crucial for containerized applications because they ensure data persistence beyond the lifecycle of a container, enabling stateful applications and data sharing across pods.

What are the persistent volumes created by the remote engine used for? \
They are used to store those setting/data that we use like odbc.ini, log files, project, DataSets, etc. We need to preserve those setting/data when container crashed or shutdown.

How do we mount those folders we need from the server into the remote engine container? \
In the screenshot, we use the --mount-dir setting when we create the docker/podman to define the folder within the server that we plan to mount onto the container. In the setting we also need to specify the path within the container that we want to use. \
![image](https://github.com/user-attachments/assets/6feff067-6ffd-428a-828f-4c1c15de3277)

This also applicable to any NFS, SMB, COS, etc if you can mount it as a folder on the server. These are some examples from Google search – \
•	Mounting an SMB Share on Linux - https://medium.com/@Josh_Rollins/mounting-an-smb-share-on-linux-57d6c2fb18e3 \
•	Mounting NFS shares on RHEL 9 - https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/managing_file_systems/mounting-nfs-shares_managing-file-systems \
•	Mounting Amazon EFS on Linux - https://docs.aws.amazon.com/efs/latest/ug/mounting-fs-mount-cmd-general.html \
•	How to mount Azure Blob Storage as a file system on Linux - https://learn.microsoft.com/en-us/azure/storage/blobs/blobfuse2-how-to-deploy?tabs=RHEL \

What are the persistent volumes created by the remote engine? \
In the screenshot, we use the --volume-dir setting when we create the docker/podman to define the folder within the server as persistent storage for the remote engine. \
![image](https://github.com/user-attachments/assets/5f0e2175-7083-4d52-814e-d9d04494469b)

What are the hostnames/URLs required for the remote engine setup? \
The server allows outbound traffic to the following URLs: \
1.	icr.io – Container repository \
2.	iam.cloud.ibm.com – Authentication with IBM Cloud \
3.	au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com – Control Plane for Sydney data center \
4.	*.cloud-object-storage.appdomain.cloud \

# Some examples of folder navigation between server and container for remote engine.

How to find the Project folder in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/PXRuntime/Projects/<ProjectID>`

How to find the Project folder in the container? \
`/ ds-storage/PXRuntime/Projects/<ProjectID>`

How to find the odbc.ini file in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/connectors/odbc/config`

How to find the odbc.ini file in the container? \
`/ds-storage/connectors/odbc/config`

How to find the job log folder in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/PXRuntime/Projects/<ProjectID>/jobs/<JobID>/runs/<JobRunID>`

How to find the job log folder in the container? \
`/ds-storage/PXRuntime/Projects/<ProjectID>/jobs/<JobID>/runs/<JobRunID>`

# Some examples on using the UI.

How to find the JobID using the UI? \
You can find it within the Project -> Jobs -> Click on the Jobs (DSFlow.DataStage job) you want to see. This same UI will project you all the job run info as well as per the screenshot below \
![image](https://github.com/user-attachments/assets/984707f1-1e84-4714-a8de-facf33b349b8)

How to see the job log using the UI? \
From the above screenshot, you just need to click on one of the job run (Mar 25, 2025 3:47:28 PM) and you will be able to see the job logs as below. \
![image](https://github.com/user-attachments/assets/d269d568-6404-4165-93e2-19ad797eb77f) \
![image](https://github.com/user-attachments/assets/e2c8a1d0-5bb6-4d15-a468-f72afd62ced8) \
![image](https://github.com/user-attachments/assets/5615c5e8-8cac-4e65-b6b8-0eebd00509e4)

How to access the project administration setting for Data Stage UI? \
You can find it within the Project you click on -> Manage -> General -> DataStage in the screenshot below. In my example, I click on a project name DSaaS Anywhere. \
![image](https://github.com/user-attachments/assets/0f104565-1908-45b1-a2a6-e143aa4851c9)

# Some examples on creating and cleanup engine

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \

To load or use the variables from the variables files.
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

In this example, I created a remote engine using the variables ${ENGINE_SYD10} which is the UNIQUE_ENGINE_NAME in my variables file. I plane to create multiple engines with difference engine name so I define multiple Engine Name variables. I also set the memory of the docker pods to 16GB and 4 vCPU as per the variables file.
```
./dsengine.sh start -n "${ENGINE_SYD10}" \
                    -a "${IBMCLOUD_APIKEY}" \
                    -e "${ENCRYPTION_KEY}" \
                    -i "${ENCRYPTION_IV}" \
                    -p "${IBMCLOUD_CONTAINER_REGISTRY_APIKEY}" \
                    --project-id "${PROJECT_PROD}" \
                    --home ${DATA_CENTER} \
                    --memory ${DS_MEMORY} \
                    --cpus ${DS_CPUS} \
                    --volume-dir ${VOLUME_DIR_SYD10} \
                    --mount-dir "${MOUNT_DIR_SYD10}"
```
