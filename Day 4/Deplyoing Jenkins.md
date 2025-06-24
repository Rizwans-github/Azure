# 🧠 Azure Virtual Machines - Session Notes

## 1. Recap of Virtualization

**What is Virtualization?**  
- Physical servers were expensive and underutilized.  
- Hypervisors logically divide one server into multiple VMs.  
- Each VM gets CPU, RAM, and storage allocation efficiently.

**How Azure Implements Virtualization:**  
- Azure uses hypervisors to partition physical servers.  
- VMs are provisioned dynamically or statically.

---

## 💻 2. Creating a Virtual Machine in Microsoft Azure

**Steps Covered:**  
- Login to Azure portal → Virtual Machines → Create  
- Select:
  - Subscription: Free Trial  
  - Resource Group  
  - VM Name, Region, Availability Zone  
  - Image: Ubuntu LTS (free eligible)  
  - Auth Type: SSH key pair  
  - VM Size: B1s  

**Pricing Notes:**  
- Free Trial: $150–$200 for 30 days  
- No charges unless upgraded  
- Billed only beyond free credits

---

## 📦 3. Types of Azure Virtual Machines

- **D-series (General Purpose)** – Balanced  
- **E-series (Memory Optimized)** – For Redis, etc.  
- **F-series (Compute Optimized)** – CPU-heavy workloads  
- **L-series (Storage Optimized)** – I/O-intensive apps  
- **N-series (GPU)** – AI/ML  
- **B-series (Budget)** – Learning/demo

---

## 🔐 4. Connecting to the VM via SSH

```bash
chmod 600 firstVM_privateKey.pem
ssh -i firstVM_privateKey.pem azureuser@<public-ip>
```

Use Git Bash (Windows) or iTerm (Mac)

---

## 🚀 5. Deploying Jenkins on the VM

**Update packages & install Java:**

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

**Install Jenkins:**

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

**Verify status:**

```bash
systemctl status jenkins
```

**Access Jenkins:**  
`http://<public-ip>:8080`

---

## 🔒 6. Opening Ports in Azure (NSG)

- Port 22 is open by default  
- Create new inbound rule:  
  - Source: Any  
  - Destination: Any  
  - Port: 8080  
  - Protocol: Any  
  - Action: Allow  

---

## 🌐 7. Introduction to Virtual Machine Scale Sets (VMSS)

- Like AWS Auto Scaling Groups  
- Automatically scales VMs up/down  
- Ideal for fluctuating traffic  
- Will be detailed in later sessions  

---

## 📝 Summary of Key Tools & Concepts

| Tool/Concept | Description |
|--------------|-------------|
| Hypervisor   | Enables virtualization |
| VM Sizes     | D, E, F, L, N series for workloads |
| SSH Keys     | Secure VM login |
| NSG Rules    | Manage network traffic |
| Jenkins      | CI/CD DevOps tool |
| VMSS         | Auto-scaling VM group |
