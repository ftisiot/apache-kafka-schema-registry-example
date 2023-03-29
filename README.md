# Apache Kafka Schema Registry Examples
A set of examples on how to use Apache Kafka schema registry functionality in [Karapace](https://www.karapace.io/)

## Setup an Apache Kafka service with Karapace

You can setup [Apache Kafka](https://hub.docker.com/r/bitnami/kafka/) and [Karapace](https://www.karapace.io/install) on Docker, however managing the integration is not trivial.

If you're not interested in the configuration details, but want a ready-to-go environment, you can use [Aiven for Apache Kafka](https://aiven.io/kafka) by:

#. Navigating to the [Aiven Console](https://console.aiven.io/), singing up for a new account and using the trial if necessary
#. Clicking on **+ Create Service**
#. Selecting **Apache Kafka**
#. Selecting the **Cloud Provider** and **Region**
#. Selecting the **Service Plan** (if you plan to test the Kafka Connect Connector notebook, you'll need a `business` plan)
#. Giving the Kafka instance a name, like `kafka-test-schema-registry`
#. The summary should look like the below

![Aiven for Apache Kafka Service Summary](/img/summary-kafka.png)

#. Clicking on **Create service**

### Customise the Aiven for Apache Kafka service to enable the Schema registry functionality

To enable the schema registry functionality you need to:

#. Navigating to the [Aiven Console](https://console.aiven.io/)
#. Navigate to the Aiven for Apache Kafka service page by clicking on the service name
#. Enabling the toggle next to **Schema Registry (Karapace)** as shown in the figure below

![Schema Registry (Karapace) toggle ON](/img/schema-registry-enabled.png)

**Note**: If you want to browse the Apache Kafka topic messages using the Aiven Console, you also need to enable the toggle next to **Apache Kafka REST API (Karapace)**

All the examples also assume you enable the `kafka.auto_create_topics_enable` toggle in the **Advanced Configuration** section.

## Download the SSL certificates and define the configuration file

### Download the SSL certificates

The SSL certificates will be used to authenticate to Aiven for Apache Kafka. You can download the certificates from the service page, as shown in the figure below. 

![Download certificates from the Aiven console](/img/certificates-download.png)


Place the certificates in the `certs` folder. You should have 3 files in the folder named:
* `ca.pem`
* `service.cert`
* `service.key`

### Edit the configuration file

The configuration file provides a way to store all the needed URI and credentials to access Aiven for Apache Kafka and the schema registry.

To create a configuration file:

* Copy `env.py.sample` to `env.py`
* Edit the parameters
    * `KAFKA_SERVICE_URI`: pointing to Apache Kafka Service URI (In the Aiven Console is  visible in the Connection information section)
      ![Aiven for Apache Kafka service console view](/img/service-uri.png)

    * `CERTIFICATES_FOLDER`: points to the folder where the certificates are stored. Should be `certs`
    * `SCHEMA_REGISTRY_HOSTNAME` and `SCHEMA_REGISTRY_PORT`: points to Karapace schema registry hostname and port (In the Aiven Console is  visible in the Connection information section, **Schema Registry** tab)
      ![Aiven for Apache Kafka Schema registry tab](/img/schema-registry-uri.png)
    * `SCHEMA_REGISTRY_USERNAME` and `SCHEMA_REGISTRY_PASSWORD` for schema registry authentication (In the Aiven Console is  visible in the Connection information section, **Schema Registry** tab)
    * `TOPIC_PREFIX` is the name of the topic that will be used to send the JSON data, and the prefix for the AVRO data


### Install required libraries

You'll need some libraries for the notebooks, install via

```
pip install -r requirements.txt
```