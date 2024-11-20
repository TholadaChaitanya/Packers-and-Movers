# **Movers and Packers Web Application**

## **Overview**
This project demonstrates a complete DevOps pipeline for the Movers and Packers web application. The web application, built using HTML, is containerized with Docker, pushed to Docker Hub, deployed on Amazon EKS, and monitored using Prometheus and Grafana.

---

## **Architecture**

![Architecture](https://github.com/user-attachments/assets/3259487f-b4cd-42f6-8937-7ee48ace2540)


---

## **1. Web Application Development**

- **Technology Stack**: HTML
- **Containerization**:
  - The web application is containerized using **Docker**.
  - Docker images are pushed to **Docker Hub** for deployment.


---

## **2. Continuous Integration (CI)**

The CI pipeline is implemented using **Jenkins**, consisting of the following stages:

1. **Git Checkout**:
   - Source code is managed on **GitHub** and pulled into Jenkins.

2. **Code Quality Analysis**:
   - **SonarQube** scans the source code to detect vulnerabilities and ensure code quality.

3. **Security Scanning**:
   - **Trivy** is used to scan:
     - **Files**: Detect vulnerabilities in the project files.
     - **Docker Images**: Scan built images for security issues.

4. **Docker Image Creation**:
   - The web application is containerized into a Docker image.

5. **Docker Image Security Scan**:
   - Post-build, the Docker image is scanned again using **Trivy**.

6. **Docker Registry Push**:
   - The Docker image is pushed to **Docker Hub**.
  


---

## **3. Continuous Deployment (CD)**

The CD pipeline leverages **GitOps** for deployment to an **Amazon EKS** cluster.

1. **Kubernetes Manifest Updates**:
   - Update Kubernetes manifests with the Docker image from Docker Hub.

2. **Manifest Push to GitHub**:
   - Updated manifests are pushed to a GitHub repository monitored by **ArgoCD**.

3. **ArgoCD Deployment**:
   - ArgoCD detects changes and deploys the containerized application to the **EKS** cluster.
  


---

## **4. Monitoring**

### **Tools Used**:
- **Prometheus**: Collects application and cluster metrics.
- **Grafana**: Visualizes the metrics collected by Prometheus.

### **Monitoring Process**:
1. **Helm Deployment**:
   - Prometheus and Grafana are deployed using **Helm charts**.
   
2. **Metrics Collection**:
   - Prometheus gathers metrics such as CPU, memory usage, and application performance.

3. **Visualization**:
   - Grafana dashboards are configured to display metrics for real-time monitoring.
  


---

## **Key Tools and Technologies**

| **Category**            | **Tool/Technology**         |
|--------------------------|-----------------------------|
| **Version Control**      | GitHub                     |
| **CI/CD Tool**           | Jenkins                    |
| **Code Quality**         | SonarQube                  |
| **Security Scanning**    | Trivy                      |
| **Containerization**     | Docker                     |
| **Container Registry**   | Docker Hub                 |
| **GitOps**               | ArgoCD                     |
| **Orchestration**        | Amazon EKS                 |
| **Monitoring**           | Prometheus, Grafana        |
| **Helm Charts**          | Used for Grafana & Prometheus deployment |

---

## **Pipeline Overview**

### **CI Pipeline**:
- Git checkout
- Code quality checks using **SonarQube**
- Security scans using **Trivy**
- Build and push Docker images to **Docker Hub**


![Jenkins](https://github.com/user-attachments/assets/2a237a2c-5bd0-4689-a0c4-af57639fba61)
  

### **CD Pipeline**:
- GitOps with **ArgoCD**
- Kubernetes deployment to **Amazon EKS**

  ![ArgoCD](https://github.com/user-attachments/assets/0172644c-a4c9-4c77-8d3f-ed07570a9f45)


### **Monitoring**:
- Metrics collection with **Prometheus**
- Dashboard visualization with **Grafana**

  <img width="959" alt="Grafana" src="https://github.com/user-attachments/assets/b8548506-f93b-4c5a-ac81-8ba1634d26fb">


---

## **Outcomes**

- **Automated CI/CD**: Reduced manual effort and ensured consistent delivery.
- **Secure Deployments**: Vulnerabilities identified and mitigated using **Trivy**.
- **Scalable Deployment**: Kubernetes on **EKS** ensured scalability and fault tolerance.
- **Real-Time Monitoring**: Prometheus and Grafana provided valuable insights into application performance.

![WebPage](https://github.com/user-attachments/assets/f8859b51-3cce-49cd-a971-cbeff92368a7)

