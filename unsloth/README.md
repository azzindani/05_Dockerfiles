# 🚀 Docker Setup for Unsloth + Jupyter Notebook (GPU-Enabled)

This guide helps you **build and run a Docker container** with GPU support for LLM training using [Unsloth](https://github.com/unslothai/unsloth), and access it via your **Chrome browser**.

---
## 📁 Step 0: Create `unsloth` Folder on Drive D:

Make sure you have a directory ready for your project.

> 💡 This is where your `Dockerfile`, notebooks, and any local files will reside.
---
## 📁 Step 1: Navigate to Your Docker Project Folder

Open **PowerShell** or **CMD** and navigate to the directory where your `Dockerfile` is located:

```terminal
d:
```
```terminal
cd unsloth
```
---

## 🛠️ Step 2: Build the Docker Image

Build the Docker image and tag it as `unsloth`:

```terminal
docker build -t unsloth .
```

> ✅ This uses the `Dockerfile` in the current folder.

---

## 🚀 Step 3: Run the Container and Launch Jupyter in Chrome

This command:

* Opens Chrome to `localhost:8888`
* Starts a Docker container with GPU support
* Mounts your local `D:\unsloth` folder to `/mnt` inside the container

```terminal
docker run -it --rm --name unsloth-gpu -p 8888:8888 --mount type=bind,source="D:\unsloth",target=/mnt --gpus all unsloth
```

---

## 🧍 Step 4: Exit the Container (When You're Done)

To **manually stop the session** and return to your local terminal, use:

```terminal
exit
```

> 💡 This command **exits the container's interactive session** and will also **stop and remove it automatically** if `--rm` was used in Step 3.

---

## 🛑 Step 5: (Optional) Stop a Running Container (Only if Detached Mode)

Only needed if you ran the container in detached mode (`-d`) **without `--rm`**:

```terminal
docker stop unsloth-gpu
```

---

## 🧹 Step 6: (Optional) Remove the Container

Run this only if the container still exists and you want to clean it up:

```terminal
docker rm unsloth-gpu
```

---
