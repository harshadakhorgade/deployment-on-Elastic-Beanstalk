# **Deploy Django on AWS Elastic Beanstalk** 🚀  

This guide provides a **step-by-step** process to **deploy a Django application** on **AWS Elastic Beanstalk (EB)** using **AWS CLI**.

---

## **1️⃣ Create IAM User and Access Key**  

1. **Go to AWS IAM Console**.  
2. **Create a new IAM User** with **AdministratorAccess** policy.  
3. **Generate an Access Key**.  
4. **Choose CLI for access**.  
5. **Save the Access Key ID and Secret Access Key**.  

---

## **2️⃣ Set Up Django Project**  

### **1. Install Dependencies**  
```sh
pip freeze > requirements.txt
```

### **2. Create `.ebextensions` Directory**  
```sh
mkdir .ebextensions
```

### **3. Add Elastic Beanstalk Configuration**  
Inside `.ebextensions/`, create a file named **`Django.config`** and add:  
```yaml
option_settings:
  aws:elasticbeanstalk:container:python:
    WSGIPath: myproject.wsgi:application
```

---

## **3️⃣ Initialize Git and AWS Elastic Beanstalk**  

### **1. Initialize Git**  
```sh
git init
git add .
git commit -m "Initial commit"
```

### **2. Initialize AWS Elastic Beanstalk**  
```sh
eb init -p python-3.11 demoapp
```
Check application on Elastic Beanstalk console on AWS.
---

## **4️⃣ Deploy to AWS Elastic Beanstalk**  

### **1. Create Environments**  
```sh
eb create production
eb create staging
```

### **2. Check Application Status**  
```sh
eb status
```

### **3. Copy CNAME and Update `settings.py`**  
Copy the **CNAME** from `eb status` and add it to `settings.py`:  
```python
ALLOWED_HOSTS = ['your-production-cname.amazonaws.com']
```

### **2. Check Application Status**  
```sh
eb status staging
```

```sh
git add .
git commit -m "CNAME added"
eb deploy production --staged
```

---

## **5️⃣ Update and Deploy Code**  

Make changes to `views.py`, commit, and deploy:  

```sh
git add .
git commit -m "Updated views"
eb deploy staging --staged
```

```sh
git add .
git commit -m "Updated views again"
eb deploy staging --staged
```

```sh
eb open staging
```

---

## **6️⃣ Monitor and Swap Environments**  

```sh
eb health staging
eb swap
```

---

## **🎯 Successfully Deployed Django on AWS Elastic Beanstalk!** 🎉
