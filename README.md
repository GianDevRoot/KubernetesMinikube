# Kubernetes Hello World (Minikube)

Este proyecto demuestra el despliegue básico de una aplicación en un clúster **Kubernetes local** utilizando **Minikube**, con el objetivo de comprender los conceptos fundamentales de *deployments*, *pods* y *services*.

---

## ⚙️ Requisitos

- Sistema operativo Linux, macOS o Windows (WSL2)
- Virtualización habilitada (VT-x / AMD-V)
- Docker o VirtualBox instalado
- `kubectl` (cliente de Kubernetes)
- `minikube` (clúster Kubernetes local)

---

## 🚀 Pasos para ejecutar

### 1. Iniciar Minikube

````
minikube start --driver=docker      # o --driver=virtualbox
````
### 2. Crear el deployment
````
kubectl apply -f hello-deployment.yaml
````

### 3. Exponer el servicio
````
kubectl expose deployment hello-deployment --type=NodePort --port=80
````

### 4. Obtener URL accesible
````
minikube service hello-deployment --url
````
Ejemplo de salida:
http://10.244.700.4:80

<p>Abra la URL en el navegador para ver el mensaje “Hello World” servido desde un contenedor Nginx dentro de Kubernetes.</p>

## 📄 Archivo hello-deployment.yaml

````
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hello
  template:
    metadata:
      labels:
        app: hello
    spec:
      containers:
      - name: hello-container
        image: nginxdemos/hello
        ports:
        - containerPort: 80
````

## ✅ Recursos Kubernetes utilizados

| Recurso    | Función                           |
|------------|-----------------------------------|
| Deployment | Define replica set declarativo    |
| Pod        | Un contenedor Nginx “hello”       |
| Service    | Expone el deployment vía NodePort |

## ¿Quieres borrar todo (deployment + service) y dejar limpio el clúster?
````
kubectl delete deployment hello-deployment
kubectl delete service hello-deployment
````

## ✍️ Autor
Giancarlos Mamani Benitez