# Web Application Monitoring Dashboard

This repository contains a complete, containerized observability stack for monitoring a FastAPI web application. It uses Prometheus to scrape application metrics and Grafana to visualize them in real-time.

## Architecture Stack

* **App:** FastAPI (Python)
* **Metrics & Time-Series DB:** Prometheus
* **Visualization:** Grafana
* **Orchestration:** Docker Compose

## Repository Structure

* `docker-compose.yaml`: The infrastructure configuration to spin up the FastAPI app, Prometheus, and Grafana containers.
* `prometheus.yml`: Configuration file for Prometheus, defining the scrape intervals and the FastAPI target endpoint.
* `fastapi-collection.json`: An API collection (e.g., Postman/Insomnia) to easily hit the FastAPI endpoints and generate traffic/metrics.
* `Web Application Monitoring Dashboard...`: final dashboard json exported

## Dashboard Metrics Summary
The included Grafana dashboard is organized into logical rows to monitor the "Golden Signals" of SRE (Latency, Traffic, Errors, and Saturation).

**1. High-Level Health (Stats)**

Process Uptime: Time elapsed since the FastAPI service started.

Total Requests: Cumulative count of all incoming HTTP traffic.

Error Rate: Percentage of requests resulting in 4xx or 5xx status codes.

Average Duration: The mean response time across all API endpoints.

Active Requests: Real-time count of concurrent requests currently being processed.

**2. Request & Traffic Analysis**

API Throughput: Time-series graph of requests per second, segmented by method, path, and status.

Status Code Distribution: A donut chart showing the breakdown of response types (e.g., 200 OK vs. 500 Internal Server Error).

**3. Performance & Latency**

Latency Percentiles (p50, p90, p95, p99): Tracks "tail latency" to identify the experience of the slowest users.

Average Duration per Route: Monitors which specific API paths are performing slower than average over time.

**4. System & Runtime Resources**

CPU & Memory Usage: Monitoring of Resident and Virtual memory, along with CPU percentage.

File Descriptors: Ratio of open files/sockets to the system limit to prevent saturation crashes.

Python Garbage Collection: Tracking of GC object collections across all three generations (0, 1, and 2) to monitor memory management overhead.

## Getting Started

### Prerequisites

* Docker
* Docker Compose

### 1. Start the Stack

Navigate to the root directory of this repository and run the following command to start all services in the background:

```bash
docker-compose up -d
```

### 2. Access the Services
Once the containers are running, you can access the services at the following local ports (adjust if your docker-compose.yaml uses different mappings):

*FastAPI Application: http://localhost:8000

*Prometheus: http://localhost:9090

*Grafana: http://localhost:3000

### 3. Cleanup

```bash
docker-compose down
