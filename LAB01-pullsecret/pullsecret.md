================
  PULL secrets
================

Pull secrets are used to access private registries.
In this case we want to access the redhat registries...

Do the following:

   oc new-project cameltest
   oc project cameltest

   oc get secret/pull-secret -n openshift-config --output=json > my-secrets.json


   NOW EDIT THE file my-secrets.json
   change the namespace setting to be that of your namespace...

   From the bottom of the file:

      "time": "2021-02-11T08:33:52Z"
           }
       ],
       "name": "pull-secret",
       "namespace": "cameltest",
       "resourceVersion": "1334",
       "selfLink": "/api/v1/namespaces/openshift-config/secrets/pull-secret",
       "uid": "3b7a9d8a-2e05-4fa5-ac85-b05dd59d5c4b"
   },
   "type": "kubernetes.io/dockerconfigjson"
}


Having done this then do the following:

#create the secret
oc create -f my-secrets.json

oc secrets link --for=pull builder pull-secret
oc secrets link default pull-secret


Congratulations you have configured a pull secret...

Now go to the docs and configure Fuse if you are using it...
https://access.redhat.com/documentation/en-us/red_hat_fuse/7.8/html/fuse_on_openshift_guide/get-started-admin#install-fuse-on-openshift4
