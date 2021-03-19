
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate \
  -DarchetypeCatalog=https://maven.repository.redhat.com/ga/io/fabric8/archetypes/archetypes-catalog/2.2.0.fuse-sb2-780040-redhat-00001/archetypes-catalog-2.2.0.fuse-sb2-780040-redhat-00001-archetype-catalog.xml \
  -DarchetypeGroupId=org.jboss.fuse.fis.archetypes \
  -DarchetypeArtifactId=spring-boot-camel-archetype \
  -DarchetypeVersion=2.2.0.fuse-sb2-780040-redhat-00001 -DgroupId=com.test -DartifactId=resttest


mvn clean install

mvn fabric8:deploy -Popenshift
