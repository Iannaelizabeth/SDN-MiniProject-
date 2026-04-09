# SDN Mininet Based Simulation – Bandwidth Measurement & Analysis

## Problem Statement

The objective of this project is to implement an SDN-based network using Mininet and an OpenFlow controller. The project demonstrates controller-switch interaction, flow rule installation, and network performance analysis using tools like `iperf`.

---

## Setup & Requirements

* Ubuntu (VM / WSL)
* Mininet
* Open vSwitch
* POX Controller (for logic implementation)
* iperf

---

## Setup Steps

### 1. Install Mininet

```bash
sudo apt update
sudo apt install mininet -y
```

### 2. Run Mininet

```bash
sudo mn --topo single,2
```

---

## Controller Logic

A custom controller (`my_controller.py`) is implemented using POX.

### Features:

* Handles `PacketIn` events
* Learns MAC-to-port mapping
* Installs flow rules using match–action logic
* Reduces controller involvement after first packet

---

## Commands Used

### Connectivity Test

```bash
pingall
```

### Bandwidth Measurement

```bash
h1 iperf -s &
h2 iperf -c h1
```

### Flow Table Inspection

```bash
sudo ovs-ofctl dump-flows s1
```

---

## Performance Analysis

| Scenario                    | Bandwidth  |
| --------------------------- | ---------- |
| Default topology            | ~900 Mbps  |
| Limited bandwidth (10 Mbps) | ~9–10 Mbps |

### Explanation:

The bandwidth was measured using iperf between hosts in Mininet.
In the default topology, high throughput was observed due to no constraints.
When bandwidth was limited using traffic control, throughput decreased significantly.
This demonstrates how network parameters affect performance in SDN environments.

---

## Test Scenarios

###  Case 1: Normal Communication

* All hosts connected
* `pingall` shows 0% packet loss

###  Case 2: Partial Failure 

* One host disconnected using:

```bash
link s1 h1 down
```

* Remaining hosts communicate successfully
* Demonstrates selective failure / blocking behavior

---

##  Observations

* Flow rules are dynamically installed by the controller
* Controller is involved only for initial packets
* Bandwidth decreases when constraints are applied
* Network behavior changes based on topology and link conditions

---

##  Proof of Execution

Screenshots included:

* Ping results (0% and partial drop)
* iperf bandwidth output
* Flow table (`ovs-ofctl dump-flows`)
* Controller logs

---

##  Conclusion

This project demonstrates how SDN enables flexible network control using centralized logic.
The results show how bandwidth and connectivity are affected by network conditions, validating the effectiveness of SDN-based management.

---

##  Files Included

* `my_controller.py` – Learning switch controller
* Screenshots of outputs

---

##  References

* Mininet Documentation
* OpenFlow Specification
* POX Controller Documentation

---
##  Screenshots

* Screenshot1=> pingall working mininet
* Screenshot2=> Pox working
* Screenshot3=> mininet with full bandwidth testing
* Screenshot4=> Pox working continued
* Screenshot5=> mininet with bw=10
* Screenshot6=> ovs-ofctl ss
* Screenshot7=> all connections working ping all(0%drop)
* Screenshot6=> one connection down(partial drop)

---

