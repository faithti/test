# TI-STACK DOCUMENTATION

## Installation
To install the TI-STACK, follow these steps:

1. Update the charts based on the contents of Chart.yaml. If you want to modify versions, make the necessary changes in Chart.yaml.

   Navigate to the folder where Chart.yaml is located and execute the following commands:
   
   ```shell
   helm dependency update
   ```
   ```shell
   helm package .
   ```
   
   This will create a .tgz file, which you will use to install the ti-stack.

2. Before proceeding with the installation, create a namespace for ti-stack. In this example, the namespace is named "monitoring" and the deployment name is "ti-stack".

   ```shell
   helm upgrade --install ti-stack ./monitoring-ti-0.1.0.tgz --namespace monitoring -f ./values.yaml
   ```

To connect to InfluxDB, use the Kubernetes service's external IP address and port. By default, the username is "admin" and the password is generated.

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

In Grafana, set InfluxDB as a datasource.

If you want to make changes to the configuration, modify the values.yaml file according to your requirements.
