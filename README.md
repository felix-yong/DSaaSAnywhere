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
In the screenshot, we use the --mount-dir setting when we create the docker/podman to define the folder within the server that we plan to mount onto the container. In the setting we also need to specify the path within the container that we want to use.

