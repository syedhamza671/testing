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

Another way to build the image:
```bash
docker build -t label .
```

---

## ⚡ Running the AutoLabeling Pipeline

### 1️⃣ **For CPU:**
```bash
docker compose run auto_labeling --autolabel "resized_frames/frames/1" "labeled_data"
```

### 2️⃣ **For GPU:**
```bash
docker compose run --gpus all auto_labeling --autolabel "resized_frames/frames/1" "labeled_data"
```
Or without using `docker-compose.yml` GPU configs:
```bash
docker run --rm --gpus all auto_labeling --autolabel "resized_frames/frames/1" "labeled_data"
```

To run Docker with X11 forwarding:
```bash
xhost +local:docker
sudo docker run --rm \
   -v $(pwd)/videos:/app/videos \
   -v $(pwd)/trimmed_videos:/app/trimmed_videos \
   -v $(pwd)/frames:/app/frames \
   -v $(pwd)/resized_frames:/app/resized_frames \
   -v $(pwd)/labeled_data:/app/labeled_data \
   -v $(pwd)/auto_labeling.sh:/app/auto_labeling.sh \
   -v /home/hamza:/app/home \
   -e DISPLAY=$DISPLAY \
   -v /tmp/.X11-unix:/tmp/.X11-unix \
   -p 8000:8000 \
   label --full_pipeline
```

---

## 🐂 Directory Structure
```
AutoLabeling_Pipeline/
│── docker-compose.yml     # Docker Compose file
│── Dockerfile             # Image build configuration
│── auto_labeling.sh       # Entry script
│── main.py                # Core processing logic
│── model_selection.py     # Model selection logic
│── requirements.txt       # Dependencies
│── videos/                # Downloaded videos
│── trimmed_videos/        # Trimmed video clips
│── frames/                # Extracted frames
│── resized_frames/        # Resized frames
│── labeled_data/          # Auto-labeled data
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

## 🛢️ Cleaning Up Docker Resources

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

## 🚩 Pipeline Commands

### 📥 Download Videos:
```bash
docker compose run auto_labeling --download
```
*Modify the `VIDEO_URLS` array in `auto_labeling.sh` to add your own URLs.*

### ✂️ Trim Videos:
```bash
docker compose run auto_labeling --trim
```
*Start and end times are pre-defined in `auto_labeling.sh`. Adjust them as needed.*

### 🎮 Extract Frames:
```bash
docker compose run auto_labeling --extract
```
*Extracts frames from the video specified in `auto_labeling.sh`.*

### 📏 Resize Frames:
```bash
docker compose run auto_labeling --resize "frames" 640 640
```
*Adjust the width and height parameters as needed.*

### 🌂 Auto-Label Frames:
```bash
docker compose run auto_labeling --autolabel "resized_frames/frames/1" "labeled_data"
```
*Ensure the `resized_frames/frames/1` directory exists with frames to be labeled.*

### ✏️ Annotate Images:
```bash
docker compose run auto_labeling --annotate "resized_frames/frames/1" "labeled_data" "annotated_output"
```

### 🚀 Run the Full Pipeline:
```bash
docker compose run auto_labeling --full_pipeline
```
*This will execute all the steps. Uncomment the necessary lines in `auto_labeling.sh` to customize the flow.*

---

## ⚙️ Environment Configuration
- **GPU Selection:**
  ```bash
  CUDA_VISIBLE_DEVICES=0 docker compose run auto_labeling --autolabel "resized_frames/frames/1" "labeled_data"
  ```
- Set `CUDA_VISIBLE_DEVICES=""` to force CPU usage.

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
  sudo chown -R $(whoami):$(whoami) /
  ```

---

## 🙌 Contributions
Feel free to fork the repo, raise issues, or submit pull requests for improvements.

