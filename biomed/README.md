# 🚀 Docker Setup for Unsloth + Jupyter Notebook (GPU-Enabled)

This guide helps you **build and run a Docker container** with GPU support for running biomedical model provided by Microsoft [microsoft/BiomedParse](https://huggingface.co/microsoft/BiomedParse), and access it via your **Chrome browser**.

---
## 📁 Step 0: Create `biomed` Folder on Drive D:

Make sure you have a directory ready for your project.

> 💡 This is where your `Dockerfile`, notebooks, and any local files will reside.
---
## 📁 Step 1: Navigate to Your Docker Project Folder

Open **PowerShell** or **CMD** and navigate to the directory where your `Dockerfile` is located:

```terminal
d:
```
```terminal
cd biomed
```
---

## 🛠️ Step 2: Build the Docker Image

Build the Docker image and tag it as `biomed`:

```terminal
docker build -t biomed .
```

> ✅ This uses the `Dockerfile` in the current folder.

---

## 🚀 Step 3: Run the Container and Launch Jupyter in Chrome

This command:

* Opens Chrome to `localhost:8888`
* Starts a Docker container with GPU support

```terminal
docker run -it --rm --name biomed-gpu -p 8888:8888 --gpus all biomed
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
docker stop biomed-gpu
```

---

## 🧹 Step 6: (Optional) Remove the Container

Run this only if the container still exists and you want to clean it up:

```terminal
docker rm biomed-gpu
```

---
