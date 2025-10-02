# 🔹 Minor Project – User Management Script (Dockerized)

This project demonstrates a **Linux user management system** wrapped in a **Docker container**.

---

## 📂 Project Structure

Minor_Project_GFG/
├── Dockerfile
├── README.md
├── user_script.sh        # Master branch - User Management
├── file_script.sh        # File branch - File System Management
├── group_script.sh       # Group branch - Group Management
├── system_script.sh      # System branch - System Performance Monitoring
├── .git/                 # Git versioning hidden folder
└── logs/                 # Optional folder for logs if you want to save outside /var/log

---

## **Step 0: Prerequisites**

1. Git installed on local machine.
2. Docker installed locally.
3. GitHub account.
4. Docker Hub account.
5. EC2 instance (Ubuntu) running with SSH access.

---

## **Step 1: Setup Git Repo Locally**

```bash
# Create project folder
mkdir Minor_Project_GFG
cd Minor_Project_GFG

# Initialize Git repo
git init
```

---

### **Step 1a: Create script files**

Create 4 scripts in this folder:

* `user_script.sh`
* `file_script.sh`
* `group_script.sh`
* `system_script.sh`

Paste your code into the respective files. Make them executable:

```bash
chmod +x *.sh
```

---

### **Step 1b: Create branch structure**

We will create **4 branches**, one for each script:

```bash
# Master branch will have user_script.sh
git checkout -b master
git add user_script.sh
git commit -m "Add user_script.sh for user management"
git branch   # should show master

# File branch
git checkout -b file
git add file_script.sh
git commit -m "Add file_script.sh for filesystem management"

# Group branch
git checkout master
git checkout -b group
git add group_script.sh
git commit -m "Add group_script.sh for group management"

# System branch
git checkout master
git checkout -b system
git add system_script.sh
git commit -m "Add system_script.sh for system performance monitoring"
```

---

### **Step 1c: Push branches to GitHub**

1. Create an empty GitHub repo: `Minor_Project_GFG`
2. Add remote and push all branches:

```bash
git remote add origin https://github.com/Zibriyal/Minor_Project_GFG.git

# Push master
git checkout master
git push -u origin master

# Push other branches
git checkout file
git push -u origin file

git checkout group
git push -u origin group

git checkout system
git push -u origin system
```

✅ Now all 4 scripts are versioned with separate branches on GitHub.

---

## **Step 2: Run scripts on EC2**

1. SSH into your EC2 instance:

```bash
ssh -i "my-key.pem" ubuntu@<EC2-PUBLIC-IP>
```
_(![alt text](<Screenshot (78)-1.png>))_

2. Update & install required tools:

```bash
sudo apt update
sudo apt install git -y
```

3. Clone your repo:

```bash
git clone https://github.com/Zibriyal/Minor_Project_GFG.git
cd Minor_Project_GFG
```

4. Run a script:

```bash
# Checkout master for user_script.sh
git checkout master
chmod +x user_script.sh
./user_script.sh
```
_(![alt text](<Screenshot (79)-1.png>))_

You can also checkout other branches to test other scripts:

```bash
git checkout file
./file_script.sh
```

---

## **Step 3: Create Dockerfile**

Inside the project folder (`Minor_Project_GFG`):

```Dockerfile
# Dockerfile
FROM ubuntu:latest
WORKDIR /usr/src/app
COPY *.sh .
RUN chmod +x *.sh
CMD ["./user_script.sh"]
```

✅ This will run `user_script.sh` by default when container starts.

---

## **Step 4: Build Docker Image Locally**

```bash
# Build Docker image
docker build -t gfg-minor-pro .

# List images
docker images
```

---

## **Step 5: Push Docker Image to Docker Hub**

```bash
# Tag image
docker tag gfg-minor-pro zibriyal/gfg-minor-pro:latest

# Login to Docker Hub
docker login

# Push image
docker push zibriyal/gfg-minor-pro:latest


```

---

## **Step 6: Pull & Run Docker Image Anywhere**

```bash
# Pull image from Docker Hub
docker pull zibriyal/gfg-minor-pro:latest
```

_(![alt text](<Screenshot (76)-1.png>))_

```bash
# Run image interactively
docker run -it zibriyal/gfg-minor-pro:latest
```

_(![alt text](<Screenshot (80)-1.png>))_


> `-it` is required for interactive scripts like your user menu.

---

## ✅ **Summary**

1. Git branch structure for 4 scripts (master, file, group, system).
2. GitHub push of all branches.
3. EC2 cloning & testing scripts.
4. Dockerfile creation & build.
5. Docker Hub push & pull.
6. Run script via Docker container interactively.

---

