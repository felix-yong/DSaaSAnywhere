# Questions and Answers

### Q01, how to find the ProjectID?
You can find it on the URL from the UI as highlighted in the screenshot below \
![image](https://github.com/user-attachments/assets/41449638-b79b-4873-b4d3-db6fd991f765) \
You can find it within the Project you click on -> Manage -> General in the screenshot below. In my example, I click on a project name DSaaS Anywhere. \
![image](https://github.com/user-attachments/assets/1cdf7552-9fe6-45fb-b7bd-44a6b6d83991)

### Q02, why we need persistent volumes for containers?
Persistent volumes are crucial for containerized applications because they ensure data persistence beyond the lifecycle of a container, enabling stateful applications and data sharing across pods.

### Q03, what are the persistent volumes created by the remote engine used for?
They are used to store those setting/data that we use like odbc.ini, log files, project, DataSets, etc. We need to preserve those setting/data when container crashed or shutdown.

### Q04, how do we mount those folders we need from the server into the remote engine container?
In the screenshot, we use the --mount-dir setting when we create the docker/podman to define the folder within the server that we plan to mount onto the container. In the setting we also need to specify the path within the container that we want to use. \
![image](https://github.com/user-attachments/assets/6feff067-6ffd-428a-828f-4c1c15de3277)

This also applicable to any NFS, SMB, COS, etc if you can mount it as a folder on the server. These are some examples from Google search –
-	Mounting an SMB Share on Linux - https://medium.com/@Josh_Rollins/mounting-an-smb-share-on-linux-57d6c2fb18e3
-	Mounting NFS shares on RHEL 9 - https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/managing_file_systems/mounting-nfs-shares_managing-file-systems
-	Mounting Amazon EFS on Linux - https://docs.aws.amazon.com/efs/latest/ug/mounting-fs-mount-cmd-general.html
-	How to mount Azure Blob Storage as a file system on Linux - https://learn.microsoft.com/en-us/azure/storage/blobs/blobfuse2-how-to-deploy?tabs=RHEL

### Q05, what are the persistent volumes created by the remote engine?
In the screenshot, we use the --volume-dir setting when we create the docker/podman to define the folder within the server as persistent storage for the remote engine. \
![image](https://github.com/user-attachments/assets/5f0e2175-7083-4d52-814e-d9d04494469b)

### Q06, what are the hostnames/URLs required for the remote engine setup?
The server allows outbound traffic to the following URLs:
1.	icr.io – Container repository
2.	iam.cloud.ibm.com – Authentication with IBM Cloud
3.	au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com – Control Plane for Sydney data center
4.	*.cloud-object-storage.appdomain.cloud

### Q07, how to create HA to ensure better availability of jobs processing?
HA for the Data Plane is built-in for deployment in K8s cluster. In term of docker/podman deployments, we need to consider the following –
- We can attach multiple remote engines to a single project.
- Each remote engine can run on difference server.
- How can the scheduling tool use difference engine to start a job when the original job start run on the pre-defined engine failed?

The above is just a simple consideration from remote engine HA perspective. There are other considerations in term of Sources/Targets locations that will impact performance when we fail-over to a difference server. \
See [Some examples on using command line cpdctl](Examples-CmdLine.md) section which we show how to run the same job on multiple engines.

### Q08, in the DSaaS service, does IBM hold any (hidden) service accounts that would be unknown to customer security personnel?

### Q09, does the IBM SaaS team hold any escalated operator privileges that would be unknown to customer security personnel?

### Q10, does continuous allow-listing of specific (external internet) domains, ports or services occur in the DSaaS service?

### Q11, does the job automatically restart when the pods crash and restart in K8s environment?
This setting APT_CHECKPOINT_RESTART will automatically restarted failed jobs due to DataStage like compute pods crash and restart. \
For failure due to the runtime pods. For more information see this [link](https://dataplatform.cloud.ibm.com/docs/content/dstage/com.ibm.swg.im.iis.ds.parjob.adref.doc/topics/checkpoint.html?context=cpdaas&locale=en&audience=wdp). \
For docker/podman, both runtime and compute are in the same pod. Automatically restart failed jobs will not work.





