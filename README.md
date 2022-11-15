# MultiCloud Workshop.

## A Day In the Serverless Life

Serverless Multicloud Development Workshop
This workshop is a series of hands-on modules which are designed to guide participants through the process of building cloud-native applications that expand across multiple clouds and platforms. The workshop provides experience using Red Hat OpenShift Container Platform, Red Hat OpenShift Serverless (Knative and Camel K), and the AMQ streams technology in Red Hat AMQ and OpenShift Streams for Apache Kafka.

:exclamation: To do this workshop we need 2 environment to be provision and are each a workshop on it own.

1. One OCP environment on Microsoft Azure
2. One OCP environment on AWS.

:warning: The 2 workshop is part of the Redhat RHPDS experience. 

#### Elements uses in the lab
    * AMQ Streams
    * Application Interconnect (Skupper)
    * Camel K
    * OpenShift Serverless
    * OpenShift Streams for Apache Kafka
    * OpenShift 4.x

__To complete the workshops some changes needs to happen__


### Administration Changes.

We need to change the _Red Hat Integration_ Operator that is provision with the workshops to version __1.8.X__. To do so follow these steps.

1. Connect to the Openshift Console as an admin.
   * The url and the admin username/password can be found in the provisionning email for the Azure workshop.

2. In the install operator tab, remove the current Red Hat Integration Operator.

3. Install the new Red Hat Integrator Operator.
![integrator_operator](/images/image1.png)

---

### Lab 01

Nothing need to be changed

---

### Lab 02

For the lab to work, we need to change the camel-k annotation found in the _MeterConsumer.java_

Change it with the following code:
```
// camel-k: language=java open-api=file:openapi-spec.yaml property=file:meters.properties build-property=quarkus.datasource.camel.db-kind=postgresql dependency=camel-openapi-java dependency=mvn:io.quarkus:quarkus-jdbc-postgresql dependency=camel:kafka dependency=camel:jdbc secret=pg-login secret=rh-cloud-services-service-account
```

:tada:   All the changes have been done, you can now continu with Lab 03.

---
### Lab 03

* For the lab to work, we need to change the camel-k annotation found in the _TollStationEventConsumer.java_

    Change it with the following code:
    ```
    // camel-k: language=java build-property=quarkus.datasource.camel.db-kind=postgresql property=file:tollstationeventconsumer.properties dependency=camel:jdbc dependency=camel:kafka dependency=mvn:io.quarkus:quarkus-jdbc-postgresql:2.0.0.Final config=secret:rh-cloud-services-service-account
    ```

* Replace _lab03_ with  lab02_ when applying the kutomize file to the project like this.

    Replace this command line:
    > oc apply -k /projects/InternationalInc/projects/lab-03/mirror-maker/ -n {username}-smartcity-central

    with:
    > oc apply -k /projects/InternationalInc/projects/lab-02/mirror-maker/ -n {username}-smartcity-central

    :warning: don't forget to replace {username} with your username.

* In the manage Kafka ckuster we need to create the edge-toll-station-events topic manually.

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

Nothing need to be changed

---
