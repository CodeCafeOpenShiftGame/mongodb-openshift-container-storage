# MongoDB with OpenShift Container Storage
This repo shows how to deploy a MongoDB container backed by OpenShift Container Storage. Red Hat's OpenShift Container Storage is software-defined storage for containers. It uses [Ceph][1] which is a battle-tested software defined storage (SDS) solution that has been available as a storage backend for OpenStack and Kubernetes for quite some time.

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

## How it works
If you look at the template you will notices that the PersistentVolume defined uses an annotation to select the storage class for CephFS - 
```
<snip>

kind: PersistentVolumeClaim
  metadata:
    annotations:
      volume.beta.kubernetes.io/storage-class: ocs-storagecluster-cephfs

<snip>
```
That's it.

You can read more about OpenShift Container Storage here:

https://www.redhat.com/en/resources/openshift-container-storage-4-datasheet

## Installing this as a template
If you are a cluster admin you can install this template to reside in the cluster (vs. git cloned and run locally) with:

`oc create -n openshift -f mongodb-ocs-persistent.yaml`

(Doing the above will just remove the need to use this github repo. Future deployments can just come straight from the cluster console or with `oc new-app --template=`).

[1]: https://www.openshift.com/blog/openshift-container-storage-4-introduction-to-ceph
