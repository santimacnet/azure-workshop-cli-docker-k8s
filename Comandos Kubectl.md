**PRACTICA COMANDOS KUBECTL GENERALES **
-------------------------------------------------------

Abrir una shell en Azure directamente para ejecutar estos comandos, necesitamos un AKS funcionando.

### Comandos para Troubleshooting and Debugging

```
attach         Attach to a running container
describe       Show details of a specific resource or group of resources
logs           Print the logs for a container in a pod
exec           Execute a command in a container
port-forward   Forward one or more local ports to a pod
proxy          Run a proxy to the Kubernetes API server
```

### Comandos get para DEPLOYMENTS, SERVICES, PODS, NAMESPACES, ETC

```
$ kubectl get pods
$ kubectl get pods -o wide
$ kubectl get pods -n kube-system
$ kubectl get pods --all-namespaces
$ kubectl get pods --all-namespaces -o wide
$ kubectl get pods --show-labels
$ kubectl get pods --watch
```

Ref: https://kubernetes.io/docs/tasks/access-application-cluster/list-all-running-container-images


### Pruebas de HelloAPP en Kubernetes

```
# Crear dos deployment directamente con "run" y nombre del pod "web" y "web2"
$ kubectl run web --image=gcr.io/google-samples/hello-app:1.0 --port=8080
$ kubectl run web2 --image=gcr.io/google-samples/hello-app:2.0 --port=8080

# Crear el service directamente con "expose" de tipo "NodePort"
$ kubectl expose deployment web --target-port=8080 --type=NodePort

# Validar que el service se ha creado correctamente y ver la IP-Externa del nodo
$ kubectl get service web
$ kubectl get svc -o wide
$ kubectl get nodes -o wide
```

### Pruebas de Cluster (GANADO vs MASCOTAS)

```
# Los PODs son mortales no resucitan, borrar un pod y ver como crea pod nuevo
$ kubectl delete pod web2-674dd45977-86s8z
$ kubectl get pods (mirar nuevo nombre y AGE)

# Los NODOS son mortales no resucitan, borrar todos los nodos de VMSS y ver que pasa
$ kubectl get nodes
$ kubectl get svc
$ kubectl get pods
$ kubectl get namespaces

# Dependerá del tipo de escalado VMSS (auto-manual) volvemos a levantar los nodos (instancias) para probar de nuevo
$ kubectl get namespaces
$ kubectl get pods
$ kubectl get svc
$ kubectl get nodes

# Preguntar al grupo que esta ocurriendo y explicar el comportamiento de Kubernetes
```