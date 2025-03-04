**Guided Activity: Getting Started with Play with Docker (PWD)**  
*Learn to run basic Docker commands for containers and images in a hands-on sandbox.*

---

### **Step 1: Access Play with Docker**
1. Go to [https://labs.play-with-docker.com/](https://labs.play-with-docker.com/).
2. Log in with your **Docker Hub account** (create one if needed).
3. Click **Start** to launch a 4-hour session (workspace resets afterward).

---

### **Step 2: Start a Terminal**
- Click **+ ADD NEW INSTANCE** to open a Linux terminal.  
  *(This is your Docker playground!)*

---

### **Step 3: Basic Docker Commands**

#### **1. Run Your First Container**
```bash
docker run hello-world
```
- **What happens?** Docker downloads the `hello-world` image and runs a container that prints a welcome message.

---

#### **2. Pull an Image**
Download the lightweight Alpine Linux image:
```bash
docker pull alpine
```
**Verify:**
```bash
docker images
```
*(Lists all images on your system)*

---

#### **3. Run a Container in Interactive Mode**
Start an Alpine container and access its shell:
```bash
docker run -it alpine sh
```
**Try:**  
```bash
echo "Hello from Alpine!" > test.txt
cat test.txt
exit
```
*(Exit the container with `exit`)*

---

#### **4. List Containers**
- **Active containers:**  
  ```bash
  docker ps
  ```
- **All containers (including stopped ones):**  
  ```bash
  docker ps -a
  ```

---

#### **5. Stop and Remove a Container**
1. Stop a running container (replace `<CONTAINER_ID>` with the ID from `docker ps`):
   ```bash
   docker stop <CONTAINER_ID>
   ```
2. Remove a stopped container:
   ```bash
   docker rm <CONTAINER_ID>
   ```

---

#### **6. Remove an Image**
```bash
docker rmi alpine
```
*(Ensure no containers using the image exist first!)*

---

### **Step 4: Advanced Practice**

#### **1. Run a Web Server (Nginx)**
```bash
docker run -d -p 80:80 --name my-nginx nginx
```
- `-d`: Run in detached mode.  
- `-p 80:80`: Map host port 80 to container port 80.  
- **Verify:** Click the **80** port link above your terminal to see the Nginx welcome page!

---

#### **2. Execute Commands in a Running Container**
Access the Nginx container’s shell:
```bash
docker exec -it my-nginx bash
```
**Try:**  
```bash
apt update  # Update package list (Ubuntu-based image)
exit
```

---

#### **3. Build Your Own Image**
1. Create a `Dockerfile`:  
   ```bash
   echo "FROM nginx:alpine
   COPY . /usr/share/nginx/html" > Dockerfile
   ```
2. Create a sample `index.html`:  
   ```bash
   echo "<h1>Hello from my custom image!</h1>" > index.html
   ```
3. Build the image:  
   ```bash
   docker build -t my-custom-nginx .
   ```
4. Run it:  
   ```bash
   docker run -d -p 8080:80 --name my-app my-custom-nginx
   ```
5. Click the **8080** port link to see your HTML page!

---

### **Step 5: Cleanup**
1. Stop all containers:  
   ```bash
   docker stop $(docker ps -aq)
   ```
2. Remove all containers:  
   ```bash
   docker rm $(docker ps -aq)
   ```
3. Remove all images:  
   ```bash
   docker rmi $(docker images -q)
   ```

---

### **Troubleshooting Tips**
- **Permission denied?** Prefix commands with `sudo` (but PWD usually doesn’t require this).
- **Port already in use?** Change the host port (e.g., `-p 8080:80`).
- **Command not found?** Check for typos!

---

### **Challenge Tasks**
1. Run a Redis container and access its CLI with `docker exec`.
2. Modify the `index.html` in your custom image and rebuild it.
3. Use `docker logs <CONTAINER_ID>` to view Nginx logs.

---

By the end of this activity, you’ll understand Docker basics like images, containers, and commands! 🐳
