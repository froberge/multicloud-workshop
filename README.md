# Serverless Multicloud Development Workshop

## A Day In the Serverless Life

This workshop is a series of hands-on modules which are designed to guide participants through the process of building cloud-native applications that expand across multiple clouds and platforms. The workshop provides experience using Red Hat OpenShift Container Platform, Red Hat OpenShift Serverless (Knative and Camel K), and the AMQ streams technology in Red Hat AMQ and OpenShift Streams for Apache Kafka.

#### Elements uses in the lab
    * AMQ Streams
    * Application Interconnect (Skupper)
    * Camel K
    * OpenShift Serverless
    * OpenShift Streams for Apache Kafka
    * OpenShift 4.x

:exclamation: To do this workshop we need 2 environments.

1. One OCP environment on Microsoft Azure
2. One OCP environment on AWS.

:warning: The 2 workshops are part of the Redhat RHPDS offering. 

---

### Lab credential:

* url : https://users-registration.apps.cluster-vlc8h.vlc8h.sandbox2113.opentlc.com
* Username: email use for registration
* Password: hybridcloud

---

__To complete the workshops some changes needs to happen__

---

### Administration changes - not required for participants.

The _Red Hat Integration_ Operator provision with the workshops need to be change to version __1.8.X__.

Steps to follow:

1. Connect to the Openshift Console as an admin.
   * The url and the admin username/password can be found in the provisionning email for the Azure workshop.

2. In the install operator tab, remove the current Red Hat Integration Operator.

3. Install the new Red Hat Integrator Operator, version _1.8.X_ with the default values.

![integrator_operator](/images/image1.png)

---

### Lab 01

No changes required

---

### Lab 02

##### One change needs to be made.

The camel-k annotation (modeline) need to be change in  _MeterConsumer.java_ for the lab to work.

Replace
` //camel-k: ... `
with
```
// camel-k: language=java open-api=file:openapi-spec.yaml property=file:meters.properties build-property=quarkus.datasource.camel.db-kind=postgresql dependency=camel-openapi-java dependency=mvn:io.quarkus:quarkus-jdbc-postgresql dependency=camel:kafka dependency=camel:jdbc secret=pg-login secret=rh-cloud-services-service-account
```

:tada:   All the changes have been done, you can now continu with Lab 03.

---
### Lab 03

##### Multiple changes needs to be made.

1. The camel-k annotation (modeline) need to be change in  _TollStationEventConsumer.java_ for the lab to work.

    Replace
    ` //camel-k: ... `
    with
    ```
        // camel-k: language=java build-property=quarkus.datasource.camel.db-kind=postgresql property=file:tollstationeventconsumer.properties dependency=camel:jdbc dependency=camel:kafka dependency=mvn:io.quarkus:quarkus-jdbc-postgresql:2.0.0.Final config=secret:rh-cloud-services-service-account
    ```

1. Replace _lab03_ with  lab02_ when applying the kutomize file to the project like this.

    Replace
    `oc apply -k /projects/InternationalInc/projects/lab-03/mirror-maker/ -n {username}-smartcity-central `
    with:
    `oc apply -k /projects/InternationalInc/projects/lab-02/mirror-maker/ -n {username}-smartcity-central`

    :warning: don't forget to replace {username} with your username.

1. In the manage Kafka cluster we need to create the edge-toll-station-events topic manually.

    * Go to the your [manage cluster](https://console.redhat.com/application-services/streams/kafkas) 

    * In your kafka instance select topic
    ![topic1](/images/image2.png)

    * select `Create topic`
        * The name to use is _edge-toll-station-events_
        * Click select and leave everything as default.
      ![topic2](/images/image3.png)


:tada:   All the changes have been done, you can now continu with Lab 04.

---

### Lab 04

No changes required

---
