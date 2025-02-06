# AutoLabeling Pipeline

## 📦 Project Overview
The **AutoLabeling Pipeline** automates the process of labeling data for computer vision tasks. It is designed to handle large datasets efficiently and supports both CPU and GPU environments using Docker.

---

## ⚙️ Prerequisites
- **Docker** and **Docker Compose** installed
- **NVIDIA Drivers** for GPU usage (with `nvidia-docker2`)
- Git for cloning the repository

### Install Docker (if not installed)
```bash
sudo apt-get update
sudo apt-get install -y docker.io docker-compose
```

### Install NVIDIA Docker (for GPU support)
```bash
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
```

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

## 📜 License
MIT License (or specify as applicable)

---

**Developed by [Your Name]**

