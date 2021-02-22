# OpenShift Tips and Tricks

## Basics

**Login**
- Retrieve token:
	- _oc whoami -t_
- Login:
	- _oc login <openshift url> --token=<token>_
- OR both at once:	
	- _oc login <openshift url> --token=$(oc whomai -t)
- OR manually via prompts
	- _oc login_


**Status / Info**
- Basic cli commands to get info
	- _oc status_
	- _oc describe_
	- _oc get <resource>_ (e.g.: _oc get project | grep scheduling_)
- Connect to a remote shell session in a pod
	- _oc rsh <pod-name>_


**Help**
- Base help command
	- _oc_
	- _oc --help_
- List types of resources (e.g. for use in _oc get_ commands)
	- _oc api-resources_
- List key terms/concepts & definitions
	- _oc types_ (deprecated)

**Create New App**
- Choose an OpenShift project (must _oc login_ first)
	- _oc project <name of project>_
- Create a deployment config
	- From a Docker image
		- _oc new-app <registry/project/image name>_
	- From a repo?????
		- _oc new-app <repo URL>_
- Expose a port on image and create an OpenShift "service" 
	- _oc expose dc/<name-of-deploymentconfig> --port=<port #>_
- Expose a port on the service and create a "route"
	- _oc expose svc/<name-of-service> --port=<port #>_


## Projects
- List projects you have permissions to view:
	- _oc projects_
- Switch projects:
	- _oc project <project name>


## Building and Pushing Docker Images
- Login
	- _docker login -p $(oc whoami -t) -u <username> <registry hostname>_
- Build (Local)
	- _docker build -t <your name>/<name of image>:latest ._
- Build (Remote)
	- _docker build -t <registry hostname>/<openshift project name>/<git repo name>:latest ._
- Push (Remote)
	- _docker push <registry hostname>/<openshift project name>/<git repo name>:latest_


## Connecting to a Pod via Port Forwarding
OpenShift does not support exposing routes via non http/tcp protocol, so
if you want to connect to, for example, a postgres DB running in a pod, it is done
via port-forwarding.

> A route is usually used for web applications which use the HTTP protocol. A route cannot be used to expose a database, as they would typically use their own distinct protocol, and routes would not be able to work with the database protocol.

https://www.openshift.com/blog/openshift-connecting-database-using-port-forwarding

- _oc login_
- _oc get pods_ (identify the postgres pod)
- _oc port-forward <pod-name> <local-port>:<remote:port>_
	- or, allow oc to choose an open local port for you: _oc port-forward <pod-name> :<remote:port>_
- _psql nameofpostgresdb username --host=127.0.0.1 --port=15432_


## Helpful Shell Aliases & Functions

```sh
alias ocl="oc login"
alias ocpb="oc project esp-scheduling-build-bdc-na"
alias ocpdt="oc project esp-scheduling-dt-bdc-na"
alias ocppt="oc project esp-scheduling-pt-bdc-na"

ocpods() {
  oc get pods | grep "$1" | cut -f 1 -d " "
}

ocrsh(){
  oc rsh $(ocpods "$1")
}

oclogs(){
  oc logs -f $(ocpods "$1")
}

ocpf(){
  oc port-forward $(ocpods "$1") "$2":"$3"
}
```
