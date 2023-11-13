# what is Garden ?
Garden.io is a cloud native application development, testing, and deployment platform. It defines the build and deployment procedure for your application in a configuration file named 'garden.yml'. It is compatible with a variety of programming languages, including JavaScript, and may be used in projects developed using React, VueJS, NodeJS, and other frontend and backend technologies.
# Why should we use it?
Garden.io makes complex app management easier by allowing you to describe all of your app's dependencies, build processes, and deployment configurations in a single configuration file.

CI/CD processes are streamlined by providing you with a configuration file that defines your pipeline's build, test, and deploy methods, automating the whole process of building, testing, and deploying your code.

Garden.io lets you design a consistent workflow for your projects, including the tools and processes for developing, testing, and delivering code. This ensures that all of your projects adhere to the same set of standards and procedures.

It supports a wide range of languages and frameworks, including Node.js, Python, and Java, making it a versatile and adaptable solution for managing and deploying your applications.
More over it keep truck on your application code and status so whenever the dev team change anything in the code , the modification is made instantly on the app on your k8s cluster (No need to push , run the pipeline again or redeploy the code )

# How does Garden work?
![Alt Text](https://github.com/jkhazri/OC-demo-Garden/blob/main/src/garden.png)

## what you need to check before preparing your deployment

**Important**: 

Please make sure you have enough resources in your Vcluseter before you start your deployment.

**Best practice :** 
You may need to limit your application ressources by adding what we called ResourceQuota kubernetes kind in your deployment Yaml file.

In this example, I've added a ResourceQuota object that sets resource limits for CPU and memory. Adjust the values based on your application's requirements. You can customize the CPU, memory and ather values according to your application's needs and the available resources in your Kubernetes cluster.

If you need to learn more about the ResourceQuota , please refer to this documentation : https://kubernetes.io/docs/concepts/policy/resource-quotas/

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: php-app-ingress
spec:
  rules:
  - host: docs-vcluster2-443.m1dns.com  # Set the desired domain or hostname here
    http:
      paths:
      - path: /
        pathType: Prefix # type the path that will be used
        backend:
          service:
            name: php-app-clusterip-service
            port:
              number: 20210
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: ingress-resource-quota
spec:
  hard:
    cpu: "500m"  # 0.5 CPU cores
    memory: "512Mi"  # 512 Megabytes of memory

```
nwo we can start :

1. Install Garden by using Installation script (Linux) :
```bash
   curl -sL https://get.garden.io/install.sh | bash
```
