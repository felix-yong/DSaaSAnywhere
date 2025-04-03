# Some examples of persistent storage and folder handling/navigation between server and container for remote engine.

### Example 01, how to find the Project folder in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/PXRuntime/Projects/<ProjectID>`

### Example 02, how to find the Project folder in the container? \
`/ ds-storage/PXRuntime/Projects/<ProjectID>`

### Example 03, how to find the odbc.ini file in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/connectors/odbc/config`

### Example 04, how to find the odbc.ini file in the container? \
`/ds-storage/connectors/odbc/config`

### Example 05, how to find the job log folder in the server where the docker/podman is running? \
`/<volume_dir>/ds-storage/PXRuntime/Projects/<ProjectID>/jobs/<JobID>/runs/<JobRunID>`

### Example 06, how to find the job log folder in the container? \
`/ds-storage/PXRuntime/Projects/<ProjectID>/jobs/<JobID>/runs/<JobRunID>`
