# TI-STACK DOCUMENTATION

## Installation
To install the TI-STACK, follow these steps:

1. Update the charts based on the contents of Chart.yaml. To modify versions, make the necessary changes in Chart.yaml. The Chart.yaml file can be found in the repository.

   Navigate to the folder where Chart.yaml is located and execute the following commands:
   
   ```shell
   helm dependency update
   ```
   ```shell
   helm package .
   ```
   This will create a .tgz file, which you will use to install the ti-stack.

2. Before proceeding with the installation, please ensure that you have created a namespace for ti-stack. In this example, we will use the namespace named *"monitoring"* and the deployment name *"ti-stack"*.

   To create the namespace, you can use the following command:

   ```shell
   kubectl create namespace monitoring
   ```

3. Once the namespace is created, you can proceed with the installation using the values.yaml file available in the repository. This values.yaml file is pre-configured with settings for Telegraf and InfluxDB based on your specific needs.

   To install ti-stack execute the following command:

   ```shell
   helm upgrade --install ti-stack ./monitoring-ti-0.1.0.tgz --namespace monitoring -f ./values.yaml
   ```
   **Note**: If you choose a different deployment name other than *"ti-stack"*, please be aware that you will need to modify the configuration in the values.yaml file accordingly.

4. To connect to InfluxDB, use the Kubernetes service external IP address and port. By default, the username is "admin" and the password is generated.

   Check the username, password, and token by executing the following commands:

   ```shell
   kubectl exec -it ti-stack-influxdb2-0 -n monitoring -- /bin/bash -c 'env | grep $DOCKER_INFLUXDB_INIT_USERNAME'
   ```
   ```shell
   kubectl exec -it ti-stack-influxdb2-0 -n monitoring -- /bin/bash -c 'env | grep $DOCKER_INFLUXDB_INIT_PASSWORD'
   ```
   ```shell
   kubectl exec -it ti-stack-influxdb2-0 -n monitoring -- /bin/bash -c 'env | grep $DOCKER_INFLUXDB_INIT_ADMIN_TOKEN'
   ```
5. In Grafana, set InfluxDB as a datasource.

To make changes to the configuration, modify the values.yaml file according to your requirements.

## About values.yaml file

By default in values.yaml file what we provided for you, Telegraf and InfluxDB are configured to meet your specific requirements. 
However, if you wish to make any changes, you can do so in the values.yaml file. Please note that if you modified the deployment name during the ti-stack installation, you will need to make additional changes. These changes include modifying environment variables and InfluxDB URLs, which will be mentioned below. 
Additionally, to enable Airflow StatsD metrics for Telegraf, you will need to make changes in the Airflow configuration.

### Configuration for Telegraf:
