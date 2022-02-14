# Readme.md

This HELM chart is a sample "as-is" chart provided to get starting with MS SQL Server (2019) deployment on Kubernetes cluster. 
 
## Prerequisites:
 
1.	This chart is built on helm v3. It requires a kubernetes cluster/Rancher/Openshift to be running for you to deploy SQL container using this chart. 
2.	Ensure you have the <b>helm</b> installed on the client from where you will connect to the kubernetes cluster to deploy using the helm chart.
3.      For continous deployments use helm upgrade (please refer to helm documentation)
4.	Requires the following variables to be set or changed in the values.yaml file :<br/> 
    a.  Please ensure that you accept the EULA for SQL Server, by changing the value of ACCEPT_EULA.value=y in values.yaml file or set it during the helm install command --set ACCEPT_EULA.value=Y.<br/> 
    b.	Please do choose the right edition of SQL Server that you would like to install you can change the value of the MSSQL_PID.value in the values file to the edition that you want to install or you can also 
        change it during the helm install command using the option --set MSSQL_PID.value=Enterprise, If you do not pass the flag and do not change it in the yaml, then by default it is going to install developer edition.<br/> c. Also please do provide your customized value for the sa_password, if you do not provide it then by default the sa_password will the value as shown in the below table.<br/> 
  
## Chart usage:
With this information, and probably after you have modified the required files you are now ready to deploy SQL Server using this chart. From the client machine where you have the helm chart installed, change the directory of the CLI to the directory where you have the chart downloaded and to deploy SQL Server using this chart run the command:


``` bash 
helm install mssql-latest-deploy . --set ACCEPT_EULA.value=Y --set MSSQL_PID.value=Developer
```
## For ex:

``` bash 
saigha01@krishna-Shibuya:~/sample-helm-chart$ helm install mssql-latest-deploy . --set ACCEPT_EULA.value=Y --set MSSQL_PID.value=Developer -n krishna-space
NAME: mssql-latest-deploy
LAST DEPLOYED: Fri Feb 11 10:56:27 2022
NAMESPACE: krishna-space
STATUS: deployed
REVISION: 1
TEST SUITE: None
```
 
After a few seconds this should deploy the SQL Server containers and you can see all the artifacts using the command :

```bash
saigha01@krishna-Shibuya:~/Documents/k8s-apps/helm-charts$ kubectl get all
NAME                                       READY   STATUS    RESTARTS   AGE
pod/mssql-latest-deploy-6745ffcf8b-bq6d4   1/1     Running   0          9m40s

NAME                          TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)          AGE
service/mssql-latest-deploy   LoadBalancer   10.43.25.136   10.10.246.203   1433:30889/TCP   9m41s

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/mssql-latest-deploy   1/1     1            1           9m40s

NAME                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/mssql-latest-deploy-6745ffcf8b   1         1         1       9m40s
```


## To remove:
``` bash 
helm uninstall mssql-latest-deploy 
```


## Connect to SQL Server

Note: Please make sure you have secured your SQL Server password according to your needs.
