# AutoLabeling Pipeline

## 📦 Project Overview
The **AutoLabeling Pipeline** automates the process of labeling data for computer vision tasks. It is designed to handle large datasets efficiently and supports both CPU and GPU environments using Docker.

---

## 🛠️ Prerequisites
Before you begin, ensure you have the following installed:

- **Docker** (latest version)
- **Docker Compose**
- **NVIDIA Container Toolkit** (if using GPU acceleration)
- **Git**

---

## 🚀 Cloning the Repository
```bash
git clone https://github.com/your-username/AutoLabeling_Pipeline.git
cd AutoLabeling_Pipeline
```

---

## 🐳 Building the Docker Image
```bash
docker compose build
```

Alternatively:
```bash
docker build -t auto_labeling .
```

---

## ⚡ Running the AutoLabeling Pipeline

### 1️⃣ **For CPU:**
```bash
docker compose run auto_labeling --autolabel "resized_frames/frames/merged_frames" "result"
```

### 2️⃣ **For GPU:**
```bash
docker compose run --gpus all auto_labeling --autolabel "resized_frames/frames/merged_frames" "result"
```
Or without using `docker-compose.yml` GPU configs:
```bash
docker run --rm --gpus all auto_labeling --autolabel "resized_frames/frames/merged_frames" "result"
```

---

## 📂 Directory Structure
```
AutoLabeling_Pipeline/
│── docker-compose.yml     # Docker Compose file
│── Dockerfile             # Image build configuration
│── auto_labeling.sh       # Entry script
│── main.py                # Core processing logic
│── requirements.txt       # Dependencies
│── data/                  # Data storage (mapped volume)
│── output/                # Results directory
```

---

## 🔍 Interacting with the Container

### Open a Bash Shell Inside the Container:
```bash
docker run -it --entrypoint /bin/bash auto_labeling
```

### Exploring Files:
```bash
ls /app
ls /var/log
```

### Listing Running Containers:
```bash
docker ps
```

### Removing Orphan Containers:
```bash
docker compose down --remove-orphans
```

---

## 🗑️ Cleaning Up Docker Resources

### Remove Unused Containers, Networks, Images:
```bash
docker system prune -a
```

### List and Remove Dangling Images:
```bash
docker images -f "dangling=true"
docker rmi $(docker images -f "dangling=true" -q)
```

---

## 🚩 Troubleshooting
- **Permission Issues:**
  ```bash
  sudo chmod 777 -R /path/to/directory
  ```
- **Check Logs:**
  ```bash
  docker logs <container_id>
  ```
- **Interactive Debugging:**
  ```bash
  docker exec -it <container_id> /bin/bash
  ```

---

## 🙌 Contributions
Feel free to fork the repo, raise issues, or submit pull requests for improvements.

