## Wordpress in kubernetes

This repository provides Kubernetes configuration files to deploy a WordPress application.These configuration files allow you to easily deploy a WordPress application with a MySQL database on a Kubernetes cluster.
Files

All the files needed to deploy Wordpress in kubernetes are given below
Configmap.yaml

In this file YAML code defines a Kubernetes ConfigMap named “mysql-config” that stores configuration data for a MySQL database. Here’s a brief explanation:

    - apiVersion and kind specify that this is a ConfigMap resource.
    - metadata provides metadata about the ConfigMap, including its name “mysql-config”.
    - data contains the configuration data as key-value pairs:
        - DATABASE: “sanjeev” (database name)
        - USER: “samir” (database user)
        - PASSWORD: “sanjeev1234” (database password)
        - ROOT_PASSWORD: “samir678” (database root password)

## Mysql_deployment.yaml

This depolyment file is defines the MySQL database deployment. Explanation of code is given below:-

   - Kind: Deployment (type of resource)
   -  Metadata: labels and name for the deployment
   - Spec:
       - Replicas: 1 (number of pods to run)
       - Selector: matches pods with label “app: mysql”
       - Template:
           - Metadata: labels for the pod
           - Spec:
               - Containers:
                   - Env: environment variables for the container (database name, user, password, root password) from the ConfigMap “mysql-config”
                   - Image: mysql:5.7 (docker image to use)
                   - Name: db (container name)
                   - Ports: 3306 (container port)

## Mysql_service.yaml

This YAML code defines a Kubernetes Service named “mysql” that exposes a MySQL database pod. Here’s a brief explanation:

    apiVersion and kind specify that this is a Service resource.
    metadata provides metadata about the Service, including its name “mysql”.
    spec defines the Service’s specifications:
        ports: exposes port 3306 (default MySQL port)
        selector: matches pods with label “app: mysql” (selects the MySQL pod to expose)

In short, this Service exposes the MySQL pod’s port 3306, making it accessible within the Kubernetes cluster.

## Wordpress_deployment.yaml

In wordpress deployment file given manifest defines Kubernetes Deployment named “wp” that runs a WordPress container. Here’s a brief explanation:

    Kind: Deployment (type of resource)
    Metadata: labels and name for the deployment
    Spec:
        Replicas: 1 (number of pods to run)
        Selector: matches pods with label “app: wordpress”
        Strategy: empty (default strategy)
        Template:
            Metadata: labels for the pod
            Spec:
                Containers:
                    Env: environment variables for the container (database host, user, password, name) from the ConfigMap “mysql-config”
                    Image: wordpress:5.2 (docker image to use)
                    Name: wordpress (container name)
                    Ports: 80 (container port)

In short, this Deployment runs a single pod with a WordPress container, using environment variables from a ConfigMap to connect to a MySQL database.

## wordpress_service.yaml

The code in this file explain the following things:-
This code creates a Kubernetes Service named “wordpress” that:

    Exposes port 80
    Selects pods labeled “app: wordpress”
    Uses a LoadBalancer for external access

In short, it exposes WordPress on port 80, making it accessible from outside the cluster.

## Steps for project:-

    1. create a repoitory in Github
    2. Clone the repository in local terminal with command git clone repository code
    3. In the directory create yaml files with vim command. The files explained above.
    4. After checking wordpress running succesfully use command git add. The git add command is used to stage changes in your working directory to the staging area. It tells Git that you want to include changes in your next commit.
    5. After adding use commit command git commit -m "any message" The git commit command is used to save changes in your staging area (index) to your local repository. It commits the changes you’ve staged with git add and creates a new commit snapshot.
    6. Use the push command . The git push command is used to upload your local repository changes to a remote repository. It updates the remote repository with your local changes, allowing others to access and collaborate on your work. git push

After that checked the repository in my GITHUB profile and all the files we created in the directory were pushed to it.
