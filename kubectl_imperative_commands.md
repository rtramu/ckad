- **kubectl set** command helps you make changes to existing application resources. Refer [here](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set) in Kubernetes official documentation to learn more. Some of the few examples below.
- **[kubectl set env](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-env-em-)** command can be used to list and update environment variables on a pod template of pod (po), replicationcontroller (rc), deployment (deploy), daemonset (ds), statefulset (sts), cronjob (cj), replicaset (rs). <br>
  Usage:
 **`kubectl set env RESOURCE/NAME KEY_1=VAL_1 ... KEY_N=VAL_N`**
  - To list the environment variables of a pod: <br>
 `kubectl set env pod \<pod_name\> --list`
  
  - To set an environment variable env=prod in all the containers in a pod: <br>
  `k set env pod \<pod_name\> -e env=prod -o yaml --dry-run=client|k replace --force -f -`

  - To import environment variable from secret: <br>
  `kubectl set env --from=secret/mysecret deployment/myapp` 

  - To import environment from a config map with a prefix: <br>
  `kubectl set env --from=configmap/myconfigmap --prefix=MYSQL_ deployment/myapp`
- **[kubectl set image](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-image-em-)** command can be used to update image on a pod template of pod (po), replicationcontroller (rc), deployment (deploy), daemonset (ds), statefulset (sts), cronjob (cj), replicaset (rs). <br>
  
  Usage: **`kubectl set image (-f FILENAME | TYPE NAME) CONTAINER_NAME_1=CONTAINER_IMAGE_1 ... CONTAINER_NAME_N=CONTAINER_IMAGE_N`**

  Examples:
  - Print result (in yaml format) of updating nginx container image from local file, without hitting the server:
  ` kubectl set image -f path/to/file.yaml nginx=nginx:1.9.1 --local -o yaml`
  - Update all deployments' and rc's nginx container's image to 'nginx:1.9.1':
  `kubectl set image deployments,rc nginx=nginx:1.9.1 --all`

- **[kubectl set resources](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-resources-em-)** command can be used to specify compute resource requirements (CPU, memory) for any resource that defines a pod template. <br>
  
  Usage: **`kubectl set resources (-f FILENAME | TYPE NAME) ([--limits=LIMITS & --requests=REQUESTS]`**

  Examples:
  - Print result (in yaml format) of updating nginx container limits from local file, without hitting the server:
  ` kubectl set resources -f path/to/file.yaml --limits=cpu=200m,memory=512Mi --local -o yaml`
  - Set a deployments nginx container cpu limits to "200m" and memory to "512Mi":
  `kubectl set resources deployment nginx -c=nginx --limits=cpu=200m,memory=512Mi`
  - Remove the resource requests and limits for resources on containers in nginx:
  `kubectl set resources deployment nginx --limits=cpu=0,memory=0 --requests=cpu=0,memory=0`
- **[kubectl set serviceaccount](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-serviceaccount-em--1)** command can be used to update service account of pod template of replicationcontroller (rc), deployment (deploy), daemonset (ds), job, replicaset (rs), statefulset. <br>
  
  Usage: **`kubectl set serviceaccount (-f FILENAME | TYPE NAME) SERVICE_ACCOUNT`**

  Examples:
  - Print result (in yaml format) of updated nginx deployment with the service account from local file, without hitting the server:
  `kubectl set sa -f nginx-deployment.yaml serviceaccount1 --local --dry-run=client -o yaml`
  - Set deployment nginx-deployment's service account to serviceaccount1:
  `kubectl set serviceaccount deployment nginx-deployment serviceaccount1`

- **[kubectl set selector](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-selector-em-)** command can be used to set the selector on a resource. Note that the new selector will overwrite the old selector if the resource had one prior to the invocation of 'set selector'. This is very useful for deployment strategies scenario. <br>
  
  Usage: **`kubectl set selector (-f FILENAME | TYPE NAME) EXPRESSIONS [--resource-version=version]`**

  Examples:
  - Set the labels and selector before creating a deployment/service pair:
  `kubectl create service clusterip my-svc --clusterip="None" -o yaml --dry-run=client | kubectl set selector --local -f - 'environment=qa' -o yaml | kubectl create -f -`

    `kubectl create deployment my-dep -o yaml --dry-run=client | kubectl label --local -f - environment=qa -o yaml | kubectl create -f -`
  