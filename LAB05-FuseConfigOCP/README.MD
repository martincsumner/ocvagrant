

//generate the project...

mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate \
  -DarchetypeCatalog=https://maven.repository.redhat.com/ga/io/fabric8/archetypes/archetypes-catalog/2.2.0.fuse-sb2-780040-redhat-00001/archetypes-catalog-2.2.0.fuse-sb2-780040-redhat-00001-archetype-catalog.xml \
  -DarchetypeGroupId=org.jboss.fuse.fis.archetypes \
  -DarchetypeArtifactId=spring-boot-camel-config-archetype \
  -DarchetypeVersion=2.2.0.fuse-sb2-780040-redhat-00001 -DgroupId=com.test -DartifactId=resttest


  mvn clean install


  oc new-project <YOURPROJECT>

 oc create -f sa.yml

 oc policy add-role-to-user view system:serviceaccount:<YOURNAMESPACE>:qs-camel-config

 mvn fabric8:deploy -Popenshift

 oc get pods

 oc logs -f conftest-1-kqz4p


description of how to do this....
https://access.redhat.com/documentation/en-us/red_hat_fuse/7.8/html/fuse_on_openshift_guide/get-started-admin#install-fuse-on-openshift4

oc create -f sample-secret.yml

REVIEW THE LOGS.....

oc create -f sample-configmap.yml

 mvn fabric8:deploy -Popenshift

 oc create -f sample-configmap.yml

 You should now see the configuration from the configmap and also the secret taking effect..
