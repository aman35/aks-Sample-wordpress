# aks-Sample-wordpress
Dynamic PVs, Ingress (nginx) are used.
Only one pod is used in each deployment.
following components created:

1)	Wordpress deployment which uses PVC
2)	Mysql deployment which uses separate pvc
3)	Env variables passed to mysql and wordpress for connections to each other
4)	2 PVC each for one deployment
5)	Storage class are created by default on AKS and dynamically provision PV when a pod utilizing PVC is created
6)	An ingress controller and ingress service (in ingress space which expose pot 80 and 443)
7)	2 services one for each deployment and both services are cluster IP type
8)	An ingress resource for wordpress service

pass following args to mysql container to avoid failures at start up:

     args:
        - "--ignore-db-dir=lost+found"
        
 example:

containers:
    - name: mysql
      image: mysql:5.7
      args:
        - "--ignore-db-dir=lost+found"
      env:
        - name: MYSQL_ROOT_PASSWORD
          value: password
