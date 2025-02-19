# 🚀 Build and Deploy a Flask App using Jenkins & Docker  

## 📌 Overview  
This guide walks you through building, testing, and deploying a simple Flask application using **Jenkins** and **Docker**.

---

## 📂 Project Structure
```
📁 my-flask-app
│── 📄 app.py # Flask application
│── 📄 test.py # Unit tests
│── 📄 requirements.txt # Python dependencies
│── 📄 Dockerfile # Docker configuration
│── 📄 Jenkinsfile # Jenkins pipeline
```

---

## 1️⃣ Setup a Simple Flask App  
- Create **`app.py`**  

---

## 2️⃣ Create a Test File  
- Create **`test.py`**  

---

## 3️⃣ Create a `requirements.txt` File  
- Define dependencies in **`requirements.txt`**  

---

## 4️⃣ Create a `Dockerfile`  
- Define container instructions in **`Dockerfile`**  

---

## 5️⃣ Build & Push Docker Image  
- Build the Docker image  
- Push the image to DockerHub  

---

## 6️⃣ Connect Jenkins Pipeline to GitHub  
1. Open **Jenkins Dashboard**.  
2. Click on **New Item** → Select **Pipeline** → Name it → Click **OK**.  
3. In the **Pipeline** section:  
   - Select **Pipeline script from SCM**.  
   - Choose **Git** as SCM.  
   - Enter your **GitHub repository URL**.  
   - Set **Branch: `main`**.  
   - Define the **Jenkinsfile path**.  
4. Click **Save**.  

---

## 7️⃣ Click "Build Now"  
- Navigate to **Jenkins Dashboard** → Your Pipeline → Click **Build Now**.  

---

🚀 **Now, your Flask app will automatically build and deploy using Jenkins & Docker!** 🚀 
