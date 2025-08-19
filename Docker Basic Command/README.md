# 🐳 Docker Commands Cheatsheet

এটি একটি **Docker Commands Cheatsheet** যেখানে Docker এর সব Basic এবং গুরুত্বপূর্ণ Command step-by-step দেওয়া আছে।


## 🔹 Docker Service Management

```bash
# Check Docker status  
sudo systemctl status docker  

# Enable Docker service  
sudo systemctl enable docker  

# Disable Docker service  
sudo systemctl disable docker  

# Start Docker service  
sudo systemctl start docker  
```

## 🔹 Docker Container Basic Commands

```bash
# Run container from image  
docker run "image_name"  
docker container run "image_name"  

# List running containers  
docker ps  
docker container ls  

# List all containers (including stopped)  
docker ps -a  
docker container ls -a  

# Run container in detached mode (background)  
docker run -d "image_name"  

# Stop a container  
docker stop "container_ID"  

# Start a stopped container  
docker start "container_ID"  

# Start container in attached mode  
docker start -a "container_ID"  

# Run container with a name  
docker run --name="custom_name" "image_name"  
```

## 🔹 Example (MongoDB Container Run)

```bash
docker run -d \
  -p 27017:27017 \
  --name mongo \
  --network mongo-network \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=qwerty \
  mongo
```

## 🔹 Container Management

```bash
# Show only container IDs  
docker ps -aq  

# Count total containers  
docker ps -aq | wc -l  

# Stop multiple containers  
docker stop $(docker ps -aq)  

# Remove container  
docker rm "container_ID"  

# Force remove container  
docker rm -f "container_ID"  

# Remove all containers  
docker rm -f $(docker ps -aq)  
```

## 🔹 Docker Images

```bash
# Pull image from DockerHub  
docker pull "image_name"  

# List all images  
docker images  
docker image ls  

# Remove image  
docker rmi "image_name"  

# Remove all images  
docker rmi $(docker images -q)  

# Force remove all images  
docker rmi $(docker images -q) -f  

# Remove unused images  
docker image prune -a  

# Remove cached & unused images  
docker system prune -af  

# Save image to tar file  
docker image save "image_name" -o "file_name.tar"  

# Load image from tar file  
docker image load -i "file_name.tar"  
```

## 🔹 Docker Volumes

```bash
# List volumes  
docker volume ls  

# Create volume  
docker volume create "volume_name"  

# Mount volume in container  
docker run -v "volume_name:/path" "image_name"  

# Mount local folder to container  
docker run -v "/local/path:/container/path" "image_name"  
```

## 🔹 Docker Networks

```bash
# Create custom network  
docker network create "network_name"  

# remove network
docker network rm "network name"

# List networks  
docker network ls  

# Use host network  
docker run --network=host "image_name"  
```

## 🔹 DockerHub Commands

```bash
# Login to DockerHub  
docker login -u "username"  

# Push image  
docker push "image_name"  

# Push image with tag  
docker push "image_name:tag"  

# Tag an image  
docker tag "old_name" "new_name"  
```

## 🔹 Useful Tips

```bash
# Run container with terminal  
docker run -t "image_name"  

# Interactive terminal  
docker run -it "image_name"  

# Exit container  
CTRL+D  

# Detach from container without stopping  
CTRL+P+Q  

# Exec into a running container  
docker exec -it "container_ID" bash  
```

## 🔹 Linux Basics (Helpful with Docker)

```bash
cd /tmp/        # Change Directory  
ls              # List files/folders  
mkdir test      # Make directory  
touch file.txt  # Create new file  
```
