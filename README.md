# MongoDB with OpenShift Container Storage
This repo shows how to deploy a MongoDB container backed by OpenShift Container Storage.

## Creating your database from this template
Just run the following:

```
oc process -f ./mongodb-ocs-persistent.yaml -l name=mongodb\
-p MONGODB_USER=thisisauser \
-p MONGODB_PASSWORD=thisis4password \
-p MONGODB_DATABASE=highscores \
-p MONGODB_ADMIN_PASSWORD=thisis4password \
| oc create -f -
```

## Installing this as a template
If you are a cluster admin you can install this template to reside in the cluster (cloned locally) with:
`oc create -n openshift -f mongodb-ocs-persistent.yaml`

(Doing the above will just remove the need to use this github repo. Future deployments can just come straight from the cluster console or with `oc new-app --template=`).