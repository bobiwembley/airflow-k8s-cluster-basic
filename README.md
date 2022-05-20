# airflow-k8s-cluster-basic


```
airflow-webserver (loadbalancer the default 8080 port with ingress controller)
airflow-scheduler
airflow-worker ( with autoscaling)
airflow-redis 
postgres ( only available on minikube & preprod env)
```

## Sandbox env.
to test and improve the configuration of your dags syntax (**airflow 2.2.4**)
You must have on your laptop **minikube**

https://minikube.sigs.k8s.io/docs/start/

to deploy sandbox you can deploy with the following command:

```
minikube status (if stopped )
minikube start
```

In **sandbox/airflow-preprod/airflow-prod** env, the configuration is set like this:

```
~/projets/gcpdw-prod/K8S/sandbox$ tree
.
├── config
│   ├── airflow-config.yml <-- create the namespace && and config service 
│   ├── airflow-secret.yml <-- git creds
│   ├── airflow-volumes.yml
│   ├── airflow-worker-hpa.yml <--autoscale of worker
│   └── roles.yml
└── resources
    ├── airflow-db.yml
    ├── airflow-redis.yml
    ├── airflow-scheduler.yml <--You can update here the git branch 
    ├── airflow-webserver.yml
    └── airflow-worker.yml
```

you have to deploy the config of the namespace dedicated to airflow 
 
```
kubectl apply -f config/
```

after that, to deploy container:

```
kubectl apply -f resources/
```

#
