# A Collection of OpenShift demos

<!-- TOC -->

- [A Collection of OpenShift demos](#a-collection-of-openshift-demos)
  - [Installing OpenShift CLI v3.11](#installing-openshift-cli-v311)
  - [OpenShift Scalability](#openshift-scalability)
  - [OpenShift Autoscaling](#openshift-autoscaling)
  - [Source to Image builds](#source-to-image-builds)
  - [Source to Image builds, with webhook triggers for builds](#source-to-image-builds-with-webhook-triggers-for-builds)
  - [Build from template for two tier -- App Server and Backend](#build-from-template-for-two-tier----app-server-and-backend)
  - [Python (Django)  - PostgreSQL Backend](#python-django----postgresql-backend)
  - [ConfigMaps](#configmaps)
  - [Persistent Storage Using Gluster - OCS](#persistent-storage-using-gluster---ocs)
  - [Persistent Storage Using NFS - OCS](#persistent-storage-using-nfs---ocs)
  - [Pipelines](#pipelines)
  - [Operators](#operators)
  - [Code Ready Workspaces](#code-ready-workspaces)
  - [Resource Quotas and Limits](#resource-quotas-and-limits)
  - [Machine Learning](#machine-learning)
  - [K-Native](#k-native)
- [Authors](#authors)

<!-- /TOC -->


### Installing OpenShift CLI v3.11
```
##Linux
curl -OL https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
tar -zxvf openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
sudo mv openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit/oc /usr/local/bin
chmod +x /usr/local/bin/oc
oc version

##MAC
curl -OL https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-mac.zip
uinzip openshift-origin-client-tools-v3.11.0-0cbc58b-mac.zip
sudo mv openshift-origin-client-tools-v3.11.0-0cbc58b-mac/oc /usr/local/bin
chmod +x /usr/local/bin/oc
oc version
```

### OpenShift Project Creation
```
oc new-project "example-project" \
  --description="Example  Description" \
  --display-name="example-project"
```

###  OpenShift User Creation
```
oc create user sample-user
```
### Update users password
```
htpasswd </path/to/users.htpasswd> sample-user
```
## Remove user from OpenShift
```
htpasswd -D </path/to/users.htpasswd> sample-user
```

### OpenShift Scalability
```
oc new-app https://github.com/sclorg/nodejs-ex
oc get pods  | grep nodejs
oc expose svc/nodejs-ex
oc scale dc nodejs-ex --replicas=3
oc get pods | grep nodejs
oc scale dc nodejs-ex --replicas=1
oc get pods | grep nodejs
oc delete all --selector app=nodejs-ex
```

### OpenShift Autoscaling
```
oc new-app https://github.com/sclorg/nodejs-ex
oc get pods  | grep nodejs
oc expose svc/nodejs-ex
oc autoscale dc/nodejs-ex --min 1 --max 5 --cpu-percent=10
oc set resources  dc/nodejs-ex --requests=cpu=200m,memory=256Mi --limits=cpu=400m,memory=512Mi

run siege
siege -r 3000 -c 50 http://urlendpoint
```

### Source to Image builds
[Source-to-Image Builders](https://github.com/tosin2013/openshift-demos/blob/master/source-to-image-demo.md)

### Source to Image builds, with webhook triggers for builds
[Source-to-Image Builders with web hooks](https://github.com/tosin2013/openshift-demos/blob/master/source-to-image-web-hooks-demo.md)

### Build from template for two tier -- App Server and Backend

### Python (Django)  - PostgreSQL Backend


### ConfigMaps
[Using ConfigMaps](https://github.com/tosin2013/openshift-demos/blob/master/configmaps.md)

### Persistent Storage Using Gluster - OCS

### Persistent Storage Using NFS - OCS

### Pipelines
https://docs.openshift.com/container-platform/3.11/dev_guide/dev_tutorials/openshift_pipeline.html
```
oc new-project test-jenkins
# If you are using minishift use
oc project myproject
oc new-app jenkins-ephemeral
oc status
oc create -f https://raw.githubusercontent.com/openshift/origin/master/examples/jenkins/pipeline/nodejs-sample-pipeline.yaml
```

### Operators
[Openshift Operators](https://github.com/tosin2013/openshift-demos/blob/master/operators/README.md)

### Code Ready Workspaces
[Download Red Hat CodeReady Workspaces](https://developers.redhat.com/products/codeready-workspaces/download/)  
[Operator Installer - 1.0.0](https://developers.redhat.com/download-manager/file/codeready-workspaces-1.0.0.GA-operator-installer.tar.gz)  
```
oc login https://master.youropenshift.com:8443
tar -zxvf codeready-workspaces-<version>-operator-installer.tar.gz
cd codeready-workspaces-operator-installer/
#optional: Modify config.yaml
./deploy.sh  --deploy config.yaml --project=your-project
```

### Resource Quotas and Limits

### Machine Learning
[MLFlow Tracking Server Operator](https://github.com/zmhassan/mlflow-tracking-operator)  
[mlflow-example](https://github.com/zmhassan/mlflow-example)

### K-Native
[Knative on an OpenShift 4.0 cluster](https://github.com/openshift-cloud-functions/Documentation/blob/master/knative-OCP-4x.md)  
[Knative Tutorial](https://redhat-developer-demos.github.io/knative-tutorial/knative-tutorial/1.0-SNAPSHOT/index.html)  
[Compile Driver](https://developers.redhat.com/coderland/serverless/)

# Authors

* **Tosin Akinosho** - *Initial work* - [tosin2013](https://github.com/tosin2013)
