# Distributed Systems Load Balancer Project 

## 📚 Table of Contents

-🤝 Collaborators

-🚀 Project Overview

-🖥️ How to Run

-🧪 Testing


## 🤝 Collaborators
### Members:
1. George Manya -148545
2. Alpha Muneeno - 144376
3. Emily Kimani - 152134
4. Kyle Waweru - 150659
   

## 🚀 Project Overview
This is a Distributed systems project that handles the implementation of a customizable load balancer with the capability of dividing the request load among N server replicas. This is useful to prevent overwhelming of a single server with a large number of server requests resulting in slower responses and potential server failure

The project utilises Docker and Flask to facilitate consistent hashing to route requests to the appropriate backend server while minimizing disruptions when servers are added or removed.

## 🔧 Software Requirements

- 🐧 **Ubuntu** 20.04 LTS or above (tested on Ubuntu 22.04)
- 🐳 **Docker** ≥ 20.10.23
- 🧱 **Docker Compose** ≥ v2.15.1
- 🐍 **Python** ≥ 3.8
- 📦 Python Packages (for analysis):
  - `aiohttp`
  - `matplotlib`

Install required Python packages:
```bash
pip install aiohttp matplotlib
````


## 🖥️ How to Run
###  Clone the repository into your maachine
`git clone https://github.com/KKXWaweru/DistributedSystems_Load_Balancer.git`




## 🛠️ Setup & Deployment

### 🧱 1. Install Docker & Compose

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER
newgrp docker
```

### ⚙️ 2. Build & Start the System

```bash
make build
make up
```

### 🔄 3. Restart / Shutdown

```bash
make restart
make down
```

---


````markdown
# 🧠 Distributed Load Balancer with Consistent Hashing

This project implements a customizable **Load Balancer** using **Consistent Hashing** to asynchronously distribute client requests across multiple Dockerized server replicas. It includes automatic scaling, fault recovery, and performance analysis.

---

## 📦 Features

- 🔁 **Load Balancing** via Consistent Hashing (`512 slots`, `9 virtual nodes per server`)
- 🐳 **Dockerized** server and load balancer containers
- 💥 **Failure Recovery**: Auto-spawns new replicas
- 📈 **Scalability Analysis** scripts with charts
- 🔌 RESTful API: `/rep`, `/add`, `/rm`, `/home`, `/heartbeat`

---

## 🚀 Project Structure

```bash
.
├── server/                     # Minimal Flask web server
│   ├── server.py
│   └── Dockerfile
├── load_balancer/             # Load balancer logic
│   ├── balancer.py
│   ├── consistent_hash.py
│   └── Dockerfile
├── analysis/                  # Task 4: Performance scripts
│   ├── test_load.py
│   ├── plot_results.py
│   └── scale_test.py
├── docker-compose.yml         # Multi-container config
├── Makefile                   # Easy commands
└── README.md
````

---

## 🛠️ Setup Instructions (Ubuntu 20.04+)

### 🧱 1. Install Docker and Compose

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER
```

### ⚙️ 2. Build and Start

```bash
make build
make up
```

### 🔄 3. Restart / Shutdown

```bash
make restart
make down
```

---

## 🔌 API Reference

### 🔹 `GET /rep`

Returns number of replicas and their hostnames.

### 🔹 `POST /add`

Add N replicas (optionally specify hostnames).

```json
{
  "n": 2,
  "hostnames": ["S4", "S5"]
}
```

### 🔹 `DELETE /rm`

Remove N replicas (optionally specify hostnames).

```json
{
  "n": 2,
  "hostnames": ["S4"]
}
```

### 🔹 `GET /home`

Routes to one of the live servers using consistent hashing.

---

## 📊 Task 4: Performance Analysis

### 🔸 A-1: Load Balance Test (N = 3)

```bash
python3 analysis/test_load.py
python3 analysis/plot_results.py
```

✅ View bar chart of requests handled per server.

---

### 🔸 A-2: Scale Test (N = 2 to 6)

```bash
python3 analysis/scale_test.py
```

✅ View line chart of average load per server as N increases.

---

### 🔸 A-3: Server Failure Recovery

```bash
docker rm -f Server1
curl http://localhost:5000/rep
```

✅ Load balancer automatically spawns a new server.

---

### 🔸 A-4: Modify Hash Functions

You can edit `consistent_hash.py`:

```python
def _hash(self, key):
    return (i + 2*i + 17) % self.slots  # Customizable
```

✅ Re-run analysis after hash function change.

---

## 🧪 Example Output (Balanced)

```json
{
  "Server1": 3321,
  "Server2": 3345,
  "Server3": 3334
}
```

---

## 🧠 Concepts Used

* Consistent Hashing (with virtual nodes)
* Docker Networking & Privileged Containers
* Fault Tolerance
* Asynchronous Request Handling (`aiohttp`)
* REST API Design



