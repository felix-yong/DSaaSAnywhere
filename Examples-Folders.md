# Some examples of persistent storage and folder handling/navigation between server and container for remote engine.

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
