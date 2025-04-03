# Some examples on creating and cleanup engine

All command in the examples here are based on variables in this file (DSaaSAnywhere_vars.sh). \
Please make sure you change all the variables to values that is applicable to your environment. \
Command reference can be find in this link - https://github.com/IBM/DataStage/tree/main/RemoteEngine/docker

### To load or use the variables from the variables files.
```
bash ./DSaaSAnywhere_vars.sh
Source ./DSaaSAnywhere_vars.sh
```

### Example 1, I created a remote engine using the variables from the variables file. I define multiple Engine Name, Volume Directory and Mount Directory variables to cater for multiple engines that I plan to create. These are the values I have set in the respective variables
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

### Example 2, I use a remote engine for difference project as indicated in the  --project-id option. These are the values I have set in the respective variables
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

### Example 3, I created the remote engine to the same project as Example 1 with a difference version of engine using the --select-version option. These are the values I have set in the respective variables
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

### You get to select which version of the engine you want to install when you set the --select-version option to true. In this example, we have 53 difference version of the engine. By default, it always install the latest version
![image](https://github.com/user-attachments/assets/ce5ec9d6-7f6b-4128-a300-51b5f31dd642)

### Example 4, I created the remote engine onto 2 projects at the same time. This remote engine can be used by both projects as per the --project-id option. These are the values I have set in the respective variables
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

### Example 5, to cleanup the engine in Example 1. These are the values I have set in the respective variables
- ${ENGINE_SYD10} is `remote_engine_ibmcloud_SYD-SYD10`
- ${DATA_CENTER} is `sydprod`

```
./dsengine.sh cleanup -n "${ENGINE_SYD10}" \
                      -a "${IBMCLOUD_APIKEY}" \
                      --project-id "${PROJECT_PROD}" \
                      --home ${DATA_CENTER}
```

### Example 6, to cleanup the engine in Example 4. These are the values I have set in the respective variables
- ${ENGINE_SYD30} is `remote_engine_ibmcloud_SYD-SYD30`
- ${DATA_CENTER} is `sydprod`

```
./dsengine.sh cleanup -n "${ENGINE_SYD30}" \
                      -a "${IBMCLOUD_APIKEY}" \
                      --project-id "${PROJECT_PROD},${PROJECT_DEV}" \
                      --home ${DATA_CENTER}
```
