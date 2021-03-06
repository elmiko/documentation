## jaeger-openshift
[github](https://github.com/jaegertracing/jaeger-openshift)
```shell
c login -u system:admin
oc new-project jaeger
oc process -f https://raw.githubusercontent.com/jaegertracing/jaeger-openshift/master/production/jaeger-production-template.yml | oc create -n jaeger -f
```
The documentation says to use cluster-admin, though this is not needed as jaeger 
is not shutting down any projects, it is only tracing the projects.

Since logging uses cluster-reader privileges, I have given jaeger the same.
```shell
oc policy add-role-to-user cluster-reader developer -n jaeger
```
Hotrods was used to test jaeger. In the hotrod example, they seem to be using hostports.

Edited the scc to enable host ports:
```shell
$ oc describe scc restricted
$ oc edit scc restricted
    allowHostPorts: true   (switched to true from false).
```
