# ESP32 Solar Tracker Web UI

![Solar Tracker Hub](https://i.imgur.com/your-image-url.png) <!-- Optional: Add a screenshot of your UI here. You can upload one to a service like imgur.com -->

This repository contains the frontend user interface for a sophisticated, DIY single-axis solar tracker powered by an ESP32 microcontroller. The UI is designed to be hosted remotely as a static site, communicating with the ESP32 backend via a RESTful API and WebSockets for real-time data.

This project is a complete management dashboard, moving beyond simple controls to include data logging, system health monitoring, and a remote event scheduler.

## 🚀 Features

*   **Real-Time Control Panel:** A dynamic, SVG-based gauge displays the panel's current angle in real-time.
*   **Historical Data Graphing:** An interactive chart visualizes the panel's position and the sun's elevation over the last 24 hours, logged to the ESP32's filesystem.
*   **System Health Dashboard:** Provides a live overview of the ESP32's operational status, including uptime, free memory, WiFi signal strength, and filesystem usage.
*   **Event Scheduler:** A full-featured UI to schedule specific actions (like moving to a set angle) to occur at a specific time and day of the week.
*   **Live Serial Monitor:** A WebSocket-based serial monitor streams log messages directly from the device to your browser.
*   **File Manager:** An interface to view, upload, and delete files on the ESP32's SPIFFS filesystem.
*   **System Configuration:** Remotely configure key parameters like GPS latitude, motor steps, and max travel angle, which are saved to the ESP32's EEPROM.
*   **Browser Notifications:** Proactively receive desktop notifications for critical system events like emergency stops or loss of connectivity.

## 🛠️ Architecture

This project utilizes a modern **decoupled frontend/backend architecture**.

*   **Backend (The Brain):** An ESP32 microcontroller running custom C++ code. It is responsible for:
    *   Controlling the stepper motor to track the sun.
    *   Reading sensor data (future-proofed).
    *   Calculating solar position based on time and latitude.
    *   Serving a JSON API and WebSocket server for real-time communication.
    *   The backend code for this project can be found in a separate repository.

*   **Frontend (This Repository):** A collection of static HTML, CSS, and vanilla JavaScript files. It is responsible for:
    *   Providing a user-friendly interface in the web browser.
    *   Fetching data from the ESP32's API endpoints.
    *   Maintaining a persistent WebSocket connection for live updates and log streaming.
    *   This UI is hosted on **Render**, providing fast load times and a seamless continuous deployment workflow.

## ⚙️ Setup & Configuration

This UI is designed to communicate with the ESP32 backend over the internet.

### 1. Backend Setup
The ESP32 must be running the corresponding server firmware and be connected to the internet. The home network router needs to be configured with:
1.  A **Dynamic DNS (DDNS)** service to provide a stable public hostname for the network (e.g., `[your-tracker.ddns.net]`).
2.  A **Port Forwarding** rule that directs traffic from an external port (e.g., port 80) to the ESP32's local IP address and port (e.g., `192.168.0.191:80`).

### 2. Frontend Configuration
Before deploying, the JavaScript files must be configured to point to the ESP32's public address. In each `.html` file, update the following constants at the top of the `<script>` section:

```javascript
const ESP32_ADDRESS = "http://[your-tracker.ddns.net]"; // Your DDNS hostname
const ESP32_WEBSOCKET = "ws://[your-tracker.ddns.net]/serial"; // WebSocket endpoint
```

## 🚀 Deployment

This project is configured for effortless continuous deployment with [Render](https://render.com/).

1.  Fork this repository to your own GitHub account.
2.  Create a new **Static Site** on Render and connect it to your forked repository.
3.  Use the following deployment settings:
    *   **Build Command:** (Leave Blank)
    *   **Publish Directory:** `.`

Any `git push` to the `main` branch of your repository will automatically trigger a new deployment on Render.

## Screenshots

*(This is a great place to add more screenshots of your different UI pages, like the history chart, health dashboard, etc.)*

*   **Control Panel**
    ![Control Panel](https://i.imgur.com/your-image-url.png)

*   **History Chart**
    ![History Chart](https://i.imgur.com/your-image-url.png)
```