# 🚑 Ambulance-to-Hospital Deterministic QoS Telemetry Framework

<p align="center">
  <strong>A Low-Latency, QoS-Aware Communication Framework for Real-Time Emergency Healthcare</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Domain-Data_Communication_Networks-blue?style=for-the-badge" alt="DCN"/>
  <img src="https://img.shields.io/badge/Application-Smart_Healthcare-red?style=for-the-badge" alt="Healthcare"/>
  <img src="https://img.shields.io/badge/Focus-Real--Time_Communication-green?style=for-the-badge" alt="QoS"/>
  <img src="https://img.shields.io/badge/Status-In_Development-orange?style=for-the-badge" alt="Status"/>
</p>

---

# 📌 Project Overview

The **Ambulance-to-Hospital Deterministic QoS Telemetry Framework** is a Data Communication and Networking (DCN) project focused on improving communication efficiency between ambulances and hospitals during emergency situations.

Modern emergency healthcare systems generate multiple types of network traffic simultaneously:

- Emergency alerts
- Patient vital-sign telemetry
- Medical records and patient identification
- Ambulance GPS location updates
- Operational status information

Under network congestion, these traffic classes compete for communication resources, potentially delaying critical emergency messages.

This project proposes a **Quality of Service (QoS) and Priority-Aware Communication Framework** that classifies ambulance-generated messages according to urgency and schedules them using deterministic priority-based packet transmission.

The objective is to ensure that life-critical patient information receives lower latency and higher delivery priority than non-critical background traffic.

---

# 🎯 Problem Statement

Traditional communication networks often process packets using First-In First-Out (FIFO) scheduling.

During congestion this may result in:

- Increased packet delay
- Queue buildup
- Higher jitter
- Delayed emergency notifications
- Reduced responsiveness of healthcare communication systems

Example:

```text
Without Prioritization

Queue:
----------------------------------------------------
Log Data | GPS | Vital Signs | ECG Alert | Status
----------------------------------------------------
        ↓
Packets are transmitted in arrival order


Even emergency alerts must wait.
```

Desired approach:

```text
With QoS-Aware Prioritization

Queue:
----------------------------------------------------
ECG Alert | Critical Vitals | GPS | Logs | Status
----------------------------------------------------
        ↓
Emergency packets transmitted first
```

---

# 💡 Proposed Solution

The framework introduces a priority-aware communication layer between ambulance systems and hospital monitoring infrastructure.

Core functions include:

### Traffic Classification

Identify message types based on urgency.

### Priority Assignment

Assign priority levels according to communication requirements.

### Packet Scheduling

Use priority-driven scheduling instead of basic FIFO transmission.

### Performance Monitoring

Measure:

- Latency
- Jitter
- Throughput
- Packet Delivery Ratio
- Packet Loss

### Comparative Analysis

Compare:

```text
FIFO Scheduling
        VS
Priority-Based Scheduling
```

to determine communication performance improvements.

---

# 🏗️ System Architecture

```text
                    Ambulance Side
 ┌─────────────────────────────────────┐
 │  Patient Monitoring Equipment       │
 │                                     │
 │  • ECG Monitor                      │
 │  • SpO₂ Sensor                      │
 │  • Blood Pressure Monitor           │
 │  • Temperature Sensor               │
 │  • GPS Unit                         │
 └────────────────┬────────────────────┘
                  │
                  ▼

       ┌────────────────────────────┐
       │ Message Classification     │
       └──────────────┬─────────────┘
                      │
                      ▼

       ┌────────────────────────────┐
       │ Priority Assignment Engine │
       └──────────────┬─────────────┘
                      │
                      ▼

       ┌────────────────────────────┐
       │ Priority Scheduler         │
       └──────────────┬─────────────┘
                      │
             Network Channel
                      │
                      ▼

      ┌──────────────────────────────┐
      │ Hospital Communication Server │
      └──────────────┬───────────────┘
                     │
                     ▼

      ┌──────────────────────────────┐
      │ Emergency Monitoring Console │
      └──────────────────────────────┘
```

---

# ⚙️ Architecture Components

| Component | Responsibility |
|------------|---------------|
| Ambulance Data Source | Generate patient telemetry |
| Message Classifier | Determine urgency level |
| Priority Manager | Assign QoS class |
| Scheduler | Select next packet |
| Communication Layer | Transport packets |
| Hospital Gateway | Receive and validate packets |
| Dashboard | Display alerts and telemetry |
| Logger | Measure network metrics |

---

# ⚡ Priority-Based Traffic Classification

## Traffic Classes

| Priority | Traffic Type | Examples | Objective |
|-----------|-------------|----------|------------|
| P1 | Critical | Cardiac arrest alert, ECG anomaly | Minimum latency |
| P2 | High | Vital-sign telemetry | Fast delivery |
| P3 | Normal | GPS updates, ETA | Standard delivery |
| P4 | Low | Diagnostic logs | Background transfer |

---

## Queue Structure

```text
Priority Queue

┌──────────────────────┐
│ P1 Critical Queue    │
├──────────────────────┤
│ P2 High Queue        │
├──────────────────────┤
│ P3 Normal Queue      │
├──────────────────────┤
│ P4 Background Queue  │
└──────────────────────┘
```

---

# 🔄 Packet Processing Workflow

```text
Generate Packet
       │
       ▼

Attach Timestamp
       │
       ▼

Classify Traffic
       │
       ▼

Assign Priority
       │
       ▼

Priority Queue
       │
       ▼

QoS Scheduler
       │
       ▼

Transmit Packet
       │
       ▼

Hospital Receiver
       │
       ▼

Calculate Metrics
```

---

# 🌐 Networking Concepts Demonstrated

## 1. Quality of Service (QoS)

QoS enables differentiated treatment of network traffic based on communication requirements.

Benefits:

- Reduced latency
- Improved responsiveness
- Better network utilization

---

## 2. Packet Scheduling

### FIFO

```text
Packet A
Packet B
Packet C

Transmit:
A → B → C
```

### Strict Priority Queue

```text
Critical
     ↓
High
     ↓
Normal
     ↓
Low
```

Critical packets are always transmitted first.

---

### Weighted Fair Queue

```text
Critical = 50%
High     = 30%
Normal   = 15%
Low      = 5%
```

Provides fairness while preserving QoS.

---

## 3. Network Congestion

When incoming traffic exceeds available bandwidth:

```text
Packet Arrival Rate
      >
Transmission Rate
```

Queue length increases, resulting in:

- Delay
- Packet loss
- Increased jitter

---

# 📏 Performance Metrics

## End-to-End Latency

```text
Latency = Receive Time - Send Time
```

```math
T_latency = T_receive - T_send
```

---

## Packet Delivery Ratio

```math
PDR = (Received Packets / Sent Packets) × 100
```

Higher PDR indicates better reliability.

---

## Throughput

```math
Throughput = Successfully Received Bits / Time
```

Measured in:

```text
bps
kbps
Mbps
```

---

## Jitter

Jitter measures packet delay variation.

```text
Packet 1 Delay = 10 ms
Packet 2 Delay = 25 ms

Jitter = 15 ms
```

Lower jitter is preferred for real-time communication.

---

# 💻 Software Architecture

```text
+--------------------------------------+
| Emergency Dashboard                  |
+--------------------------------------+
| Hospital Receiver                    |
+--------------------------------------+
| Network Communication Layer          |
+--------------------------------------+
| QoS Scheduler                        |
+--------------------------------------+
| Traffic Classification Engine        |
+--------------------------------------+
| Ambulance Telemetry Generator        |
+--------------------------------------+
```

---

# 🧩 Core Data Structures

## Packet Structure

```c
typedef struct
{
    uint32_t packet_id;

    uint32_t timestamp;

    uint8_t priority;

    char message[128];

} Packet_t;
```

---

## Priority Queue Structure

```c
typedef struct
{
    Packet_t packets[100];

    int front;

    int rear;

} PriorityQueue_t;
```

---

# 💻 Code Implementation Examples

## Traffic Classification

```c
uint8_t classify_packet(Packet_t *packet)
{
    if(packet->type == C*ITICAL_ALERT)
        return PRIOR*TY_P1;

    if(packet->type == VIT*L_SIGN)
        return PRIORITY_P2*

    if(packet->type == GPS_UPDAT*)
        return PRIORITY_P3;

   *return PRIORITY_P4;
}
```

---

##*Priority Scheduling

```c
Packet_t*schedule_packet(void)
{
    if(!qu*ue_empty(P1))
        return deque*e(P1);

    if(!queue_empty(P2))
 *      return dequeue(P2);

    if(*queue_empty(P3))
        return de*ueue(P3);

    return dequeue(P4);*}
```

---

## Latency Calculation*
```c
double calculate_latency(
  * uint32_t tx,
    uint32_t rx)
{
 *  return (double)(rx - tx);
}
```
*---

## Packet Delivery Ratio

```*
double calculate_pdr(
    uint32_* sent,
    uint32_t received)
{
  * return ((double)received /
      *     (double)sent) * 100.0;
}
```
*---

# 🧪 Experimental Methodology*
## Baseline

### FIFO Scheduling
*```text
All packets share a single*queue
```

Purpose:

- Establish b*seline performance

---

## Propos*d

### QoS Priority Scheduling

``*text
Separate queues
Priority-awar* transmission
```

Purpose:

- Red*ce critical-message latency

---

*# Test Scenarios

| Scenario | Net*ork Load | Objective |
|----------*|-------------|-----------|
| S1 |*Low | Baseline behavior |
| S2 | M*derate | Queue analysis |
| S3 | H*gh | Congestion analysis |
| S4 | *ixed Traffic | Emergency prioritiz*tion |
| S5 | Packet Loss | Reliab*lity testing |
| S6 | Persistent C*itical Traffic | Fairness evaluati*n |

---

# 📊 Results Visualizati*n

Recommended plots:

### Latency*vs Traffic Load

```text
Traffic L*ad
      │
      │
      │
      │*      └────────────►
```

### Thro*ghput Comparison

```text
FIFO
QoS*Priority
```

### PDR Comparison

*``text
Packet Delivery Ratio (%)
`*`

### Priority-Wise Delay

```tex*
P1 Delay
P2 Delay
P3 Delay
P4 Del*y
```

---

# 🔐 Reliability and S*curity Considerations

Future vers*ons should include:

- Message aut*entication
- AES encryption
- TLS *ommunication
- Packet integrity va*idation
- Duplicate detection
- Re*ry mechanisms
- Queue overflow pro*ection
- Failure recovery strategi*s

---

# 📁 Repository Structure
*```text
ambulance-hospital-qos-fra*ework/

├── README.md

├── docs/
│*  ├── network_design.md
│   ├── sy*tem_architecture.md
│   └── experi*ental_methodology.md

├── src/
│   ├── ambulance/
│   ├── hospital/
│   ├── scheduler/
│   └── common/

├── simulation/
│   ├── scenarios/
│   └── configurations/

├── tests/

├── data/
│   └── sample_logs/

├── results/
│   ├── metrics/
│   └── figures/

├── scripts/

├── requirements.txt

└── LICENSE
```

---

# 🎓 Learning Outcomes

This project demonstrates:

- Data Communication and Networking
- Quality of Service (QoS)
- Priority-Based Scheduling
- TCP/IP Communication
- UDP Communication
- Queue Management
- Congestion Control
- Traffic Engineering
- Real-Time Telemetry
- Healthcare Communication Systems
- Performance Evaluation
- Network Simulation
- Latency Analysis

---

# 🚀 Future Enhancements

- ESP32-based ambulance telemetry node
- STM32 medical sensor integration
- MQTT communication support
- DSCP-enabled QoS routing
- Adaptive priority scheduling
- Multi-hospital communication
- Multi-ambulance simulation
- Edge AI emergency prediction
- Secure encrypted communication
- Real-world network emulation

---

# 🌍 Real-World Relevance

This project bridges academic networking concepts with practical healthcare communication systems.

Applications include:

- Emergency ambulance telemetry
- Smart healthcare networks
- Real-time IoT systems
- QoS-aware communication protocols
- Medical network research
- Edge-enabled healthcare infrastructure

The framework serves as a research and educational platform for studying how deterministic communication and QoS mechanisms can improve emergency information delivery under network congestion.

---

# 👨‍💻 Author

**Naveen Karan R S**

B.Tech – Electronics and Communication Engineering

- GitHub: https://github.com/naveenkaranrs
- LinkedIn: https://www.linkedin.com/in/naveenkaran2005

> Engineering low-latency communication frameworks for time-critical healthcare systems through QoS, traffic scheduling, and real-time networking.

---

# 📄 License

Distributed under the MIT License.

See the `LICENSE` file for details.
