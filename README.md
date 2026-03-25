# IoT Real-Time Monitoring: Socket to MQTT with Grafana

## Project Overview
This project demonstrates an IoT data pipeline that transfers real-time sensor data through multiple stages: from a local socket sensor to an edge device, then to a cloud MQTT broker, and finally to a Grafana monitoring dashboard.

### System Architecture & Data Flow
1.  **Laptop 1 (Sensor):** Runs `socket_sensor.py`. It generates temperature data and sends it via **Python Sockets** to Laptop 2.
2.  **Laptop 2 (Edge Device):** Runs `edge_device.py`. It listens for incoming socket data and forwards (publishes) it to the **MQTT Broker**.
3.  **Laptop 1 (Main Server + Grafana):** Subscribes to the MQTT broker and visualizes the live data stream on a **Grafana Dashboard**.

---

## Configuration
*   **Socket Connection:** `localhost:5000` (for single-machine testing) or `Laptop2_IP:5000`.
*   **MQTT Broker:** `broker.emqx.io`
*   **MQTT Port:** `1883`
*   **MQTT Topic:** `savonia/iot/temperature`

---

## Grafana Dashboard
The dashboard is configured with two main panels:
1.  **Temperature Live Data (Time Series):** Shows the real-time trend of temperature over the last 5 minutes.
2.  **Current Temperature (Gauge):** Displays the most recent value with color-coded thresholds (Green for normal, Yellow/Red for high).

**Note on Limitation:** This setup uses the MQTT Data Source for **live monitoring**. Data is not stored historically in Grafana unless a time-series database (like Loki or InfluxDB) is added to the pipeline.

### Dashboard Screenshot
![Grafana Dashboard](https://raw.githubusercontent.com/eurusfox-24/ai_product_agent/main/Desktop/Wireless%2C%20RT/MQTT%20exercises/mqtt_pub_ss.png)
*(Replace with your actual dashboard screenshot if different)*

---

## Reflection Questions

**1. What is the role of Grafana in this system?**
Grafana acts as the **user interface (UI)**. It takes raw data from the MQTT broker and transforms it into visual charts or gauges, making it easy for humans to monitor the system's status in real time.

**2. Why is MQTT useful for monitoring applications?**
MQTT is a **lightweight** protocol designed for constrained devices and low-bandwidth networks. Its **Publish/Subscribe** model allows many sensors to send data independently, and multiple dashboards can subscribe to that data simultaneously without direct connections to the sensors.

**3. What is the difference between live monitoring and historical storage?**
*   **Live Monitoring:** Displays data as it arrives in real time. If the dashboard is closed, the previous data points are lost.
*   **Historical Storage:** Saves all incoming data into a **database**. This allows for long-term trend analysis, reporting, and debugging issues that happened in the past.

---

## Project Files
*   `socket_sensor.py`: Generates and sends data via Socket.
*   `edge_device.py`: Receives Socket data and publishes to MQTT.
*   `README.md`: System documentation and lab report.
