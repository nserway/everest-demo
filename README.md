# Vision

This repository includes several demos of the [EVerest](https://lfenergy.org/projects/everest/) tech stack capabilities which aim to examplify the modular nature of EVerest. The intent of the repository is to showcase the foundational layers of a charging solution that could address interoperability and reliability issues in the industry. The demonstrations can be utilized to better understand the following: 

- Standards-based implementations for driving interoperability between the EV, EVSE, and CSMS
- Interoperability testing tools and test suites
- Simulated EVs, EVSEs, etc. following interoperability best practices and simulating non happy-path charginig scenarios.

# Hardware Specific Insructions

- Mac OS
- Linux
- Windows

# Install

Install docker with the following link: [Get Docker](https://docs.docker.com/get-docker/)
   
- Insure that the terminal has access to `docker` and `docker compose`
 
# STEP 1: Select the Demo 

Below is a table of demonstrations that are currently available. Copy and paste the command in the far right column for the demo you wish to execute. 
| Demo | Content | Diagram | Command |
| ---- | ---- | ---- | ---- |
| **One EV ↔ EVSE (AC Simulations)** | | |  |
| **One EV ↔ EVSE (ISO 15118-2 DC)** | |
| **Two EV ↔ EVSE** | 
- Copy and paste the command for the demo you want to see:
    - 🚨 AC Charging ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-ac.sh | bash`
    - 🚨 ISO 15118 DC Charging ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-dc.sh | bash`
    - 🚨 Two EVSE Charging ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-two-evse.sh | bash`
    - 🚨 E2E Automated Tests ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-automated-testing.sh | bash`
    - 🚨 Basic and ISO 15118-2 AC Charging with OCPP 1.6J CSMS (StEVe) ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-ac-plus-ocpp.sh | bash -s -- -j`
    - 🚨 Basic and ISO 15118-2 AC Charging with OCPP 2.0.1 CSMS (MaEVe Security Profile 1) ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-ac-plus-ocpp.sh | bash -s -- -1` 
    - 🚨 Basic and ISO 15118-2 AC Charging with OCPP 2.0.1 CSMS (MaEVe Security Profile 2) ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-ac-plus-ocpp.sh | bash -s -- -2`
    - 🚨 Basic and ISO 15118-2 AC Charging with OCPP 2.0.1 CSMS (MaEVe Security Profile 3) ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-ac-plus-ocpp.sh | bash -s -- -3`
    - 🚨 Basic and ISO 15118-2 AC Charging with OCPP 2.0.1 CSMS (CitrineOS Security Profile 1) ⚡: `curl https://raw.githubusercontent.com/everest/everest-demo/main/demo-iso15118-2-ac-plus-ocpp.sh | bash -s -- -c -1`

> NOTE: the `Basic and ISO 15118-2 AC Charging with OCPP 1.6J CSMS (StEVe)` demo is known to fail intermittently, and will not be fixed.

### STEP 2: Interact with the demo
- Open the `nodered` flows to understand the module flows at http://127.0.0.1:1880
- Open the demo UI at http://127.0.0.1:1880/ui
- When running the Basic and ISO 15118-2 AC Charging with OCPP 1.6J CSMS demo, you can open the SteVe wep portal at http://localhost:8180/steve/manager/home. Login with username: admin, password: 1234
- When running the Basic and ISO 15118-2 AC Charging with OCPP 201 CSMS demo, the script currently checks out the maeve repository and builds it, so it is fairly slow.
  - It starts the Maeve containers in detached mode, so you would need to use docker desktop or `docker logs` to see the logs
  - Note that the OCPP logs are available at `/tmp/everest_ocpp_logs/` on the EVerest manager and can be downloaded using the docker desktop or `docker cp`

| Nodered flows | Demo UI | Including simulated error |
 |-------|--------|------|
 | ![nodered flows](img/node-red-example.png) | ![demo UI](img/charging-ui.png) | ![including simulated error](img/including-simulated-error.png) |

 | SteVe web portal |
 |-------|
 | ![SteVe web portal](img/steve-web-portal.png) |

 | OCPP 201 with successful connection |
 |-------|
 | ![OCPP 201 connection](img/ocpp201-connection.png) |
 

### STEP 3: See the list of modules loaded and the high level message exchange
![Simple AC charging station log screenshot](img/simple_ac_charging_station.png)

### OPTIONAL: Explore the configs visually
- This demo can be run independently, and exports [the admin panel](https://everest.github.io/nightly/general/03_quick_start_guide.html#admin-panel-and-simulations) as explained [in this video](https://youtu.be/OJ6kjHRPkyY?t=904).It provides a visual representation of the configuration and the resulting configurations.
- Run the demo: 💄 exploring configs 🔧: `curl -o docker-compose.yml https://raw.githubusercontent.com/everest/everest-demo/main/docker-compose.admin-panel.yml && docker compose -p everest-admin-panel up`
- Access the visual representation at http://localhost:8849

### TEARDOWN: Clean up after the demo
- Kill the demo process
- Delete files and containers: `docker compose -p [prefix] down && rm docker-compose.yml`
where `[prefix]` is `everest, everest-dc, everest-two-evse...`

## High level block diagram overview of EVerest capabilities
From https://everest.github.io/nightly/general/01_framework.html
![image](https://everest.github.io/nightly/_images/quick-start-high-level-1.png)

## Notes for Demo Contributors
Docker images defined in this repository are built during pull requests, on merges to `main`, and on pushes of semantic version tags. The labels for newly-built images are determined by the `TAG` environment variable specified in the root level `.env` file in this repository. The value of `TAG` is also used throughout the demo `docker-compose.*.yml`.
