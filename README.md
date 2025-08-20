# InstructLab Pipelines

## Build Custom Workbench Image

```
source .env
cd docker
podman build -t quay.io/oawofolurh/agentic-wb:latest .
podman push quay.io/oawofolurh/agentic-wb:latest
cd -
```

OR

```
oc new-build --name=data-prep-wb --to="quay.io/oawofolurh/agentic-wb:latest" --strategy=docker --binary
oc start-build data-prep-wb --from-dir docker --follow
```

## Deploy Workbench
* Use the image built above to import a new notebook image
	* Attach a GPU accelerator profile if one exists
2. When creating the workbench in the Web GUI Console:
	* Use the following script to generate the **wb-secret.yaml** file to attach to the workbench:
	
	```
	oc create secret generic data-prep-wb --from-env-file .env
	oc get secret data-prep-wb -oyaml > openshift/wb-secret.yaml
	```
