### [My GitHub](https://github.com/omarwarsame)
### [My LinkedIn](https://www.linkedin.com/in/owarsame/)
### [Drop me a line](mailto:jubawarsame@gmail.com)
### [My Resume](https://devsom.co.uk/)
# 3 Tier Todo App
***


## PHP To-do application requirements
This app will require database and database management tool

## What this app can do
It can insert data, update data and delete data
***
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
***
## DEPLOYMENT PROCESS
### Step 1:
#### MYSQL POD
##### Parameters Required:
1. Database Name
2. Username
3. Password

_Database Name = sqldb_.
_Database User = root_.
_Root Password = rootpassword_.


### STEP 2:
#### PHPMYADMIN POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database Username
4. Database Password

Link it with MSQL
phpMyAdmin is a Database management tool.


### STEP 3:
#### PHP To-Do App POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database User
4. User Password.
Link it with MYSQL

***
***
***
> "Live as if you were to die tomorrow. Learn as if you were to live forever." – Mahatma Gandhi



