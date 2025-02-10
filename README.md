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
docker build -t auto_labeling .
```
---

## ⚡ Running the AutoLabeling Pipeline

*It will Automatically switched to GPU if available othervise it'll use CPU*

### 1️⃣ **Using Docker Compose (with `docker-compose.yml`):**

```bash
docker compose run auto_labeling --autolabel
```
### 2️⃣ **Using Docker (without `docker-compose.yml`):**
without using `docker-compose.yml` GPU configs and To run Docker with X11 forwarding:
```bash
xhost +local:docker
sudo docker run --rm \
   -v $(pwd)/videos:/app/videos \
   -v $(pwd)/trimmed_videos:/app/trimmed_videos \
   -v $(pwd)/frames:/app/frames \
   -v $(pwd)/resized_frames:/app/resized_frames \
   -v $(pwd)/labeled_data:/app/labeled_data \
   -v $(pwd)/auto_labeling.sh:/app/auto_labeling.sh \
   -v $(pwd)/pipeline/model_selector.py:/app/pipeline/model_selector.py \
   -v $(pwd)/pipeline/helper.py:/app/pipeline/helper.py \
   -v $(pwd)/pipeline/tool.py:/app/pipeline/tool.py \
   -e DISPLAY=$DISPLAY \
   -v /tmp/.X11-unix:/tmp/.X11-unix \
   -p 8000:8000 \
   auto_labeling --full_pipeline
```

---

## 🐂 Directory Structure
```
AutoLabeling_Pipeline/
├── docker-compose.yml       # Docker Compose file
├── Dockerfile               # Image build configuration
├── auto_labeling.sh         # Entry script
├── pipeline/                # Pipeline scripts
│   ├── main.py              # Core processing logic
│   ├── model_selector.py    # Model selection logic
│   ├── tool.py              # Helper tools
│   └── helper.py            # Additional helpers
├── requirements.txt         # Dependencies
├── videos/                  # Downloaded videos
├── trimmed_videos/          # Trimmed video clips
├── frames/                  # Extracted frames
├── resized_frames/          # Resized frames
└── labeled_data/            # Auto-labeled data
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

### Available Options:
- **Download Videos**
- **Trim Videos**
- **Extract Frames**
- **Resize Frames**
- **Auto-Label Frames**
- **Annotate Images**
- **Run the Full Pipeline**

### 🚀 Example: Run the Full Pipeline
```bash
docker compose run auto_labeling --full_pipeline
```
*This will execute all the steps. Uncomment the necessary lines in `auto_labeling.sh` to customize the flow.*

---

## ⚙️ Environment Configuration
- **GPU Selection:**
  - Set `CUDA_VISIBLE_DEVICES=0` to use GPU in `docker-compose.yml`.
  - Set `CUDA_VISIBLE_DEVICES=""` to force CPU usage in `docker-compose.yml`.
- **GPU Selection:**
  - To transfer ownership of all the directories and files created via Docker.
 ```bash
  sudo chown -R $(whoami):$(whoami) /
  ```


