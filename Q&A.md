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
