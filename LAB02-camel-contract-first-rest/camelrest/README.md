----------------------
Camel Contract First. / DEBUG project
======================


1.  BeerWebEndpoint is a code generation from a swagger document.
    beer-svc-impl is the implementation of that same service.

2.  mvn clean install - will perform the code gen and package appropriately.

3.  We now want to deploy this in such a way that we can build locally and then be able to profile or debug...

4.  The dockerfile under the implementation allows us to include agents into the build for this very purpose..


Commands to deploy using Openshift's Binary build.

oc new-build --strategy docker --binary --docker-image registry.redhat.io/fuse7/fuse-java-openshift --name beerservice
oc set build-secret --pull bc/beerservice pull-secret


mvn clean install...
oc start-build beerservice --from-dir .  --follow


//can we deploy directly from the generated config. - this does not map the ports or add the liveness probes.
oc new-app beerservice

oc expose svc/beerservice
oc get route beerservice

Environvars - add these to the deployment-config.

 for debuggging : JAVA_TOOL_OPTIONS = -agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n

 for profiling : JAVA_TOOL_OPTIONS =  -agentpath:/usr/local/YourKit-JavaProfiler-2019.8/bin/linux-x86-64/libyjpagent.so=port=10001,listen=all

Debugging....

oc port-forward mytestapp-4-cqg76 8000:8000

(mytestapp-4-cqg76 is the name of the pod you wish to debug)


set up a remote debugger -- pointing to the locally forwarded port
we can use the locally running fabric8 plugin to generate resources for us....
