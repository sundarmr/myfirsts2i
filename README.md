oc new-build registry.access.redhat.com/jboss-amq-6/amq63-openshift:1.2~https://github.com/sundarmr/myfirsts2i.git -e environment=dev
oc create -n broker1 -f ../../templates/p66-amq63-persistent.yaml
oc create configmap p66-amq-configs --from-file=p66.properties=../../config/p66-dev.properties
oc policy add-role-to-user view -z default
oc new-app --template "broker1/p66-amq63-persistent"
