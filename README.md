# DSaaSAnywhere

This is a documentation related to DataStage as a Service Anywhere

# Information / Reference

Supported Kubernetes (K8s) Services (See this link for latest update) – (Info below is as of 20250328) \
- OpenShift \
- IBM K8s Services (IKS) \
- Amazon Elastic K8s Services (EKS) \

Supported OS (See this link for latest update) for docker/podman– (Info below is as of 20250328) \
- Red Hat Enterprise Linux (RHEL) 8.8, 8.10, 9.2 and 9.4 \
-	Ubuntu 20.04, 22.04, 24.04 \

URL for SYD Data Center of CPDaaS/DSaaS – au-syd.dai.cloud.ibm.com and api.au-syd.dai.cloud.ibm.com

DSaaS Anywhere LI – https://www.ibm.com/support/customer/csol/terms/?id=i126-9243&lc=en

SLA for IBM Cloud (See this link for latest update) – DSaaS is Tier 3 at 99.99% (Info is as of 20250328). The following are some pointers to read the link. \
-	See Section 4 for the SLAs availability. \
-	See Section 6 for the Supported SLA Tiers by service. DataStage is at pg 11 of 19. \

Documentation link to DSaaS – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/datastage.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS Anywhere remote engine – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/create-remote-engine.html?context=cpdaas&audience=wdp \
-	Direct link for Docker – https://github.com/IBM/DataStage/tree/main/RemoteEngine/docker \
-	Direct link for K8s – https://github.com/IBM/DataStage/tree/main/RemoteEngine/kubernetes \
Documentation link to FAQ for DSaaS Anywhere – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/remote_engine_faqs.html?context=cpdaas&audience=wdp \
Documentation link to security for DSaaS Anywhere remote engines – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/security_for_remote_runetime_engines.html?context=cpdaas&audience=wdp \
Documentation link on sharing the remote engines across projects – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/sharing_remote_engine.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS command-line tools – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/cli.html?context=cpdaas&audience=wdp \
Documentation link to DSaaS APIs – https://dataplatform.cloud.ibm.com/docs/content/dstage/dsnav/topics/ds-apis.html?context=cpdaas&audience=wdp

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

# [Questions and Answers](Q&A.md)

# [Some examples on using UI](Examples-UI.md)
# Some examples on using the UI.
# [Some examples on creating and cleanup engine](Examples-Engines.md)
# Some examples on creating and cleanup engine

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
Command reference can be find in this link - https://github.com/IBM/DataStage/tree/main/RemoteEngine/docker

To load or use the variables from the variables files.
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

Example 1, I created a remote engine using the variables from the variables file. I define multiple Engine Name, Volume Directory and Mount Directory variables to cater for multiple engines that I plan to create. These are the values I have set in the respective variables \
- ${ENGINE_SYD10} is `remote_engine_ibmcloud_SYD-SYD10`
- ${DS_MEMORY} is `16G`
- ${DS_CPUS} is `4`
- ${DATA_CENTER} is `sydprod`
- ${VOLUME_DIR_SYD10} is `/EnginePV/SYD-SYD10`
- ${MOUNT_DIR_SYD10} is `/opt/SYD-SYD10:/ds-storage/SYD-SYD10`

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

Example 2, I use a remote engine for difference project as indicated in the  --project-id option. These are the values I have set in the respective variables \
- ${ENGINE_SYD10} is `remote_engine_ibmcloud_SYD-SYD20`
- ${DS_MEMORY} is `16G`
- ${DS_CPUS} is `4`
- ${DATA_CENTER} is `sydprod`
- ${VOLUME_DIR_SYD20} is `/EnginePV/SYD-SYD20`
- ${MOUNT_DIR_SYD20} is `/opt/SYD-SYD20:/ds-storage/SYD-SYD20`

```
./dsengine.sh start -n "${ENGINE_SYD20}" \
                    -a "${IBMCLOUD_APIKEY}" \
                    -e "${ENCRYPTION_KEY}" \
                    -i "${ENCRYPTION_IV}" \
                    -p "${IBMCLOUD_CONTAINER_REGISTRY_APIKEY}" \
                    --project-id "${PROJECT_DEV}" \
                    --home ${DATA_CENTER} \
                    --memory ${DS_MEMORY} \
                    --cpus ${DS_CPUS} \
                    --volume-dir ${VOLUME_DIR_SYD20} \
                    --mount-dir "${MOUNT_DIR_SYD20}"
```

Example 3, I created the remote engine to the same project as Example 1 with a difference version of engine using the --select-version option. These are the values I have set in the respective variables \
- ${ENGINE_SYD11} is `remote_engine_ibmcloud_SYD-SYD11`
- ${DS_MEMORY} is `16G`
- ${DS_CPUS} is `4`
- ${DATA_CENTER} is `sydprod`
- ${VOLUME_DIR_SYD11} is `/EnginePV/SYD-SYD11`
- ${MOUNT_DIR_SYD11} is `/opt/SYD-SYD11:/ds-storage/SYD-SYD11`
- ${REMOTE_ENGINE_BATCH_SIZE} is `10`
- ${VERSION} is `true`

```
./dsengine.sh start -n "${ENGINE_SYD11}" \
                    -a "${IBMCLOUD_APIKEY}" \
                    -e "${ENCRYPTION_KEY}" \
                    -i "${ENCRYPTION_IV}" \
                    -p "${IBMCLOUD_CONTAINER_REGISTRY_APIKEY}" \
                    --project-id "${PROJECT_PROD}" \
                    --home ${DATA_CENTER} \
                    --memory ${DS_MEMORY} \
                    --cpus ${DS_CPUS} \
                    --volume-dir ${VOLUME_DIR_SYD11} \
                    --mount-dir "${MOUNT_DIR_SYD11}" \
                    --env-vars REMOTE_ENGINE_BATCH_SIZE=${REMOTE_ENGINE_BATCH_SIZE} \
                    --select-version ${VERSION}
```

You get to select which version of the engine you want to install when you set the --select-version option to true. In this example, we have 53 difference version of the engine. By default, it always install the latest version \
![image](https://github.com/user-attachments/assets/ce5ec9d6-7f6b-4128-a300-51b5f31dd642)

Example 4, I created the remote engine onto 2 projects at the same time. This remote engine can be used by both projects as per the --project-id option. These are the values I have set in the respective variables \
- ${ENGINE_SYD30} is `remote_engine_ibmcloud_SYD-SYD30`
- ${DS_MEMORY} is `16G`
- ${DS_CPUS} is `4`
- ${DATA_CENTER} is `sydprod`
- ${VOLUME_DIR_SYD11} is `/EnginePV/SYD-SYD11`
- ${MOUNT_DIR_SYD11} is `/opt/SYD-SYD11:/ds-storage/SYD-SYD11`
- ${REMOTE_ENGINE_BATCH_SIZE} is `10`
  
```
./dsengine.sh start -n "${ENGINE_SYD30}" \
                    -a "${IBMCLOUD_APIKEY}" \
                    -e "${ENCRYPTION_KEY}" \
                    -i "${ENCRYPTION_IV}" \
                    -p "${IBMCLOUD_CONTAINER_REGISTRY_APIKEY}" \
                    --project-id "${PROJECT_DEV},${PROJECT_PROD}" \
                    --home ${DATA_CENTER} \
                    --memory ${DS_MEMORY} \
                    --cpus ${DS_CPUS} \
                    --volume-dir ${VOLUME_DIR_SYD30} \
                    --mount-dir "${MOUNT_DIR_SYD30}" \
                    --env-vars REMOTE_ENGINE_BATCH_SIZE=${REMOTE_ENGINE_BATCH_SIZE}
```

Example 5, to cleanup the engine in Example 1. These are the values I have set in the respective variables \
- ${ENGINE_SYD10} is `remote_engine_ibmcloud_SYD-SYD10`
- ${DATA_CENTER} is `sydprod`

```
./dsengine.sh cleanup -n "${ENGINE_SYD10}" \
                      -a "${IBMCLOUD_APIKEY}" \
                      --project-id "${PROJECT_PROD}" \
                      --home ${DATA_CENTER}
```

Example 6, to cleanup the engine in Example 4. These are the values I have set in the respective variables \
- ${ENGINE_SYD30} is `remote_engine_ibmcloud_SYD-SYD30`
- ${DATA_CENTER} is `sydprod`

```
./dsengine.sh cleanup -n "${ENGINE_SYD30}" \
                      -a "${IBMCLOUD_APIKEY}" \
                      --project-id "${PROJECT_PROD},${PROJECT_DEV}" \
                      --home ${DATA_CENTER}
```





