Here's a basic `README.md` file for **Task 3 – Infrastructure as Code (IaC) with Terraform** using Docker. It explains the objective, setup, steps, and verification.

---

### 📄 `README.md`

````markdown
# Task 3: Infrastructure as Code (IaC) with Terraform and Docker

## ✅ Objective
Provision a local Docker container using Terraform.

## 🛠️ Tools Used
- Terraform
- Docker
- Ubuntu EC2 instance (AWS)

## 📁 Files
- `main.tf`: Contains Terraform code to provision Docker image and container.
- Terraform CLI output logs (`init`, `plan`, `apply`, `destroy`).

## 📦 Docker Details
- **Image**: `nginx:latest`
- **Container Name**: `nginx-container`
- **Exposed Port**: 80 (Docker) → 80 (Host)

---

## 🚀 Steps Performed

1. **Terraform Init**
   ```bash
   terraform init
````

2. **Terraform Plan**

   ```bash
   terraform plan
   ```

3. **Terraform Apply**

   ```bash
   terraform apply
   ```

   ✅ This pulls the `nginx` image and runs a container with port 80 exposed.

4. **Verify the Container**

   * Used: `docker ps` to confirm container is running.
   * Verified in browser using: `http://<EC2-Public-IP>:80`
     → Nginx Welcome Page appeared.

5. **Terraform Destroy (optional)**

   ```bash
   terraform destroy
   ```

---

## 📌 Terraform Code (`main.tf`)

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {
  host = "unix:///var/run/docker.sock"
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx" {
  name  = "nginx-container"
  image = docker_image.nginx.name

  ports {
    internal = 80
    external = 80
  }
}
```

---

## 🔒 Security Group Note (AWS EC2)

Make sure the security group associated with the EC2 instance has **port 80 open** for **0.0.0.0/0** to allow HTTP access.

---

## ✅ Outcome

Successfully provisioned and deployed an Nginx container using Terraform as Infrastructure as Code (IaC). Verified through browser access and container logs.

```

---

```
