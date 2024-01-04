# 3 Tier Todo App



## PHP To-do application requirements
This app will require database and database management tool

## What this app can do
It can insert data, update data and delete data
_________________________________________________________________________________________________________

## Kubernetes

### MYSQL POD
#### Required
1. ConfigMap
2. Secret
3. ClusterIP Service

### PHPMYADMIN POD
#### Required
1. ConfigMap
2. Secret
3. NodePort Service

### PHP Todo App POD
#### Required
1. NodePort Service
_________________________________________________________________
## DEPLOYMENT PROCESS
### Step 1:
#### MYSQL POD
##### Parameters Required:
1. Database Name
2. Username
3. Password

   Database Name = sqldb
   Database User = root
   Root Password = rootpassword


### STEP 2:
#### PHPMYADMIN POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database Username
4. Database Password
___Link it with MSQL___
phpMyAdmiin is a Database management tool.


### STEP 3:
#### PHP To-Do App POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database User
4. User Password
___Link it with MYSQL




