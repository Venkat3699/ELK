Install EFK/ELK by using Helm

1. To Create the namespace for ELK
    ```
    kubectl create ns elk
	kubectl get ns
    ```

2. Add the elastic search repo
	```
    helm repo add elastic https://helm.elastic.co
    helm repo ls
	helm show values elastic/elasticsearch >> elasticsearch.values
    vim elasticsearch.values
	```
	- update replicas & minimum Master nodes and Resources requests & limits (Min Memory 2Gi) in elasticsearch.values
	```
	helm install elasticsearch elastic/elasticsearch -f elasticsearch.values -n elk
    helm ls -n elk
    kubectl get all -n elk
	```
3. Edit kibana values file 
    ```
    helm show values elastic/kibana >> kibana.values
    vim kibana.values
    ```
    - Resources requests & limits (Memory 1Gi) & in Service type as NodePort/LoadBalancer and port as 80.
    ```
    helm install kibana elastic/kibana -f kibana.values -n elk

4. Install FileBeat
    ```
    helm install filebeat elastic/filebeat -n elk
    helm ls -n elk
    kubectl get all -n elk
    kubectl get pvc -n elk
    kubectl get pv -n elk
    ```
##### Optional 
    ```
    helm show values elastic/metricbeat >> metricbeat.values
    # Update hostNetworking as true
    helm install metricbeat elastic/metricbeat -f metricbeat.values -n elk
