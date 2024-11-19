
# **Mini-Stream**

**Mini-Stream** is a streaming and processing framework, combining features from **SciStream** and **APS Mini-App**. It is the integration of [Scistream](https://github.com/scistream/scistream-proto) and [aps-mini-app](https://github.com/diaspora-project/aps-mini-apps) to replicate the data production, and streaming to be processed in another location. It is designed for high-performance, distributed data streaming applications, enabling modular, efficient, and scalable workflows.

---

## **Features**
- **SciStream Integration**:
  - Streamlined producer-to-consumer communication.
  - Secure and efficient data transmission through high performance tunneling.
  - Flexible configurations for multi-network setups.

- **APS Mini-App Integration**:
  - Advanced data reconstruction and quality analysis using SIRT (Simultaneous Iterative Reconstruction Technique).
  - Modular Python-based services for tomographic data streaming, distribution, and reconstruction.
  - Compatibility with large datasets and high computational demands.

---

## **Architecture**
The `mini-stream` project consists of the following components:
1. **S2CS**
   - Scistream Control Server that manages the proxy configuration to connect the producer and receiver.
2. **Producer**:
   - The raw data is created (simulated) via aps-mini-app's Data Acquisition (daq) service.
   - The data is then processed and distributes via mini-app's Data Distributor (dist) service.
   - Finally, producer, streams raw data for processing to the consumer using the Scistream architecture.
3. **Receiver**:
   - Recieves the data from the Scistream tunnel.
   - It is then reconstructed and stored for further processing via aps-mini-app's Reconstruction (sirt) service.

The architecture is designed to handle modular service orchestration using `docker-compose`.

---

## **Requirements**
### **System Requirements**
- Docker 20.x or later
- Docker Compose v2.0 or later
- At least 4 GB of free memory and 15-20 GB of disk space
- Python 3.11

---

## **Installation**
### **1. Clone the Repository**
```bash
git clone https://github.com/seenv/mini-stream.git
cd mini-stream
```

### **2. Build the Docker Images**
Run the following command to build all services:
```bash
docker-compose -f ./docker-compose-3.yaml build
```

### **3. Start the Services**
Start all services using Docker Compose:
```bash
docker-compose -f ./docker-compose-3.yaml up
```

---

## **Usage**
### **Running the Services**
- **Producer**:
  Producer of the raw data to be processed.
- **p2cs and s2cs**:
  Scistream control server.
- **ministream**:
  Simulates, Processes, and distributes the data for reconstruction.
  Performs reconstruction and stores the output.
- **Receiver**:
  Receiver and consumer side that processes the raw data.

You can monitor logs for each service:
```bash
docker-compose logs -f producer
docker-compose logs -f p2cs
docker-compose logs -f c2cs
docker-compose logs -f receiver
docker-compose logs -f ministream
```

### **Customizing the Configuration**
- Update `docker-compose.yaml` for network and container configurations.
- Edit Python scripts in the `aps-mini-apps` directory for custom logic.

### **Data Directory**
Mount a volume for output data:
```yaml
volumes:
  output_data:
    driver: local
```

Access output data in `/mnt/output` inside the container.

---

## **Development**
### **Building Individual Images**
To rebuild a specific service:
```bash
docker-compose build <service-name>
```

### **Debugging**
Attach a shell to a running container:
```bash
docker exec -it <container-name> /bin/bash
```

---

## **Acknowledgments**
- [SciStream](https://github.com/scistream/scistream-proto): Advanced data streaming framework.
- [APS Mini-App](https://github.com/diaspora-project/aps-mini-apps): A modular tomographic processing tool.

