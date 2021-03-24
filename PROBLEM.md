## Exercise: Experiment with Ingress and autoscaling a Spring Boot application on K8s Cluster in Azure AKS.

  
* In this exercise, you will practice how to configure Ingress and auto-scaling on a K8s Cluster in Azure AKS.
* You will use Kubernetes Horizontal Pod Autoscaler (HPA) for auto-scaling.


This exercise contains following folders:

	- service-app - A SpringBoot microservice
	- k8-manifests - A folder that contains the manifest files
  
  This exercise contains the following files in k8-manifests folder:

	- springboot-deployment.yml - To create the Deployment
	- springboot-svc.yml - To create the Service of type ClusterIP
	- springboot-ingress.yml - To create the Ingress
	
**Note**: You need to go through the comments thoroughly and complete the exercise.

To define Deployment and Service, understand and perform following steps:

	1. Build `springboot-app` Docker image for service-app microservice and push it to Docker Hub.
	2. Define a Deployment named `springboot-deployment` in `springboot-deployment.yml` with 1 replica. Use the image created in the preceding step.
	3. Define a Service named `springboot-svc` in `springboot-svc.yml` for the deployment created in step 2.
	4. Define an Ingress named `springboot-ingress` in `springboot-ingress.yml`.

Understand and perform following steps to complete the exercise:

1. Open terminal and and cd into the folder where manifest files are present.
2. Verify that the AKS cluster is created and is ready.
3. Implement `springboot-deployment.yml` to define the Deployment.
4. Implement `springboot-svc.yml` to define the Service.
5. Install `helm` in your local machine to enable the Ingress Controller. If you have already installed, you can skip this step. (Reference for installing helm is given below).
6. Create the Ingress Controller in default namespace. (Reference to create the ingress controller is given below).
7. Implement `springboot-ingress.yml` to define the Ingress.
8. Capture the `EXTERNAL-IP` of your `nginx-ingress-controller`. Access `http://<EXTERNAL-IP>/api/v1/hello` in the browser and verify the result.
9. To deploy the metrics server, run `kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.6/components.yaml`.
10. To verify metrics-server deployment status, run the command `kubectl get deployment metrics-server -n kube-system`.
11. Run kubectl autoscale command for autoscaling. Ensure that autoscaling gets triggered when CPU usage reaches 50%. Also ensure that the minimum and maximum number of pods to create are five and ten respectively.
12. Get the current status of Autoscaler.
13. Run the load-generator in 2 different terminals to start new containers.
14. To send requests to the server, run the command `while true; do wget -q -O - http://<Ingress-Controller-EXTERNAL-IP>/api/v1/hello; done` in the terminals opened in step 14.
15. Run the command `kubectl get hpa -w`. You will see HPA scale the pods from 1 up to our configured maximum (10) until the CPU average is below our target (50%).
16. You can stop the load test that was running in the other terminal. You will notice that HPA will slowly bring the replica count to min number based on its configuration. You should also get out of the load testing application by pressing Ctrl + D.
17. Run the command `kubectl get pods` to see the pods scaling down.

## Reference

- [Install helm](https://helm.sh/docs/intro/install/)
	- Install helm `From Apt (Debian/Ubuntu)`
- [Create an ingress controller](https://docs.microsoft.com/en-us/azure/aks/ingress-basic)
	- The above link has a command for creating a new namespace, you can ignore that and create ingress controller in default namespace.

## Instructions

- Take care of white space/trailing whitespace
- Do not change the provided class/method names unless instructed
- Ensure your code compiles without any errors/warning/deprecations
- Follow best practices while coding
