# Docker and Kubernetes Installation using MicroK8s

This guide walks through the installation and setup of Docker and Kubernetes (via MicroK8s) on a Linux system. It covers both the installation of Docker and setting up Kubernetes using MicroK8s.

---

## Prerequisites

- A system running Linux (Ubuntu or a Debian-based distribution).
- Sudo privileges.

---

## Step 1: Install Docker

Docker is essential for containerized applications. Follow these steps to install Docker:

1. **Update the package index**:
    ```bash
    sudo apt update
    ```

2. **Install Docker**:
    ```bash
    sudo apt install docker.io
    ```

3. **Start Docker and enable it to start on boot**:
    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

4. **Verify Docker installation**:
    ```bash
    docker --version
    ```
    You should see the installed Docker version.

5. **Add your user to the `docker` group**:
    ```bash
    sudo groupadd docker
    sudo usermod -aG docker $USER
    ```

6. **Apply the changes**:
    Log out and log back in, or use the following command:
    ```bash
    su - $USER
    ```

7. **Test Docker**:
    Run a test container:
    ```bash
    docker run hello-world
    ```

---

## Step 2: Install Kubernetes using MicroK8s

MicroK8s is a lightweight, simple-to-install version of Kubernetes. Follow these steps to install and set it up:

1. **Install MicroK8s**:
    ```bash
    sudo snap install microk8s --classic
    ```

2. **Add your user to the MicroK8s group**:
    ```bash
    sudo usermod -aG microk8s $USER
    su - $USER
    ```

3. **Verify MicroK8s installation**:
    Check the status of MicroK8s:
    ```bash
    microk8s status --wait-ready
    ```

4. **Enable essential addons**:
    Enable DNS and storage addons for Kubernetes functionality:
    ```bash
    microk8s enable dns storage
    ```

5. **Verify Kubernetes nodes**:
    ```bash
    microk8s kubectl get nodes
    ```

6. **Check running pods in all namespaces**:
    ```bash
    microk8s kubectl get pods -A
    ```

7. **Set up `kubectl` alias (optional)**:
    If you prefer to use `kubectl` instead of `microk8s kubectl`, set up an alias:
    ```bash
    sudo snap alias microk8s.kubectl kubectl
    ```

---

## Step 3: Test Kubernetes Deployment

To verify that Kubernetes is working, you can deploy a simple NGINX web server:

1. **Create an NGINX deployment**:
    ```bash
    microk8s kubectl create deployment nginx --image=nginx
    ```

2. **Check the deployment**:
    ```bash
    microk8s kubectl get deployments
    ```

3. **Expose the deployment as a service**:
    ```bash
    microk8s kubectl expose deployment nginx --port=80 --target-port=80 --type=ClusterIP
    ```

4. **Verify the service**:
    ```bash
    microk8s kubectl get services
    ```

---

## Conclusion

You've successfully installed Docker and Kubernetes (MicroK8s). You can now start deploying and managing your containerized applications using Kubernetes.

--- 

### Notes

- To check the status of MicroK8s and ensure everything is running fine:
    ```bash
    microk8s status --wait-ready
    ```

- Remember to use `microk8s kubectl` for all Kubernetes commands unless you set up an alias for `kubectl`.

---

### License
This guide is licensed under the MIT License.
