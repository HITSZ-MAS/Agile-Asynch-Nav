<div align="center">
  
  <h1>Agile in the Face of Delay</h1>
  <h2>Asynchronous End-to-End Learning for Real-World Aerial Navigation</h2>

  <p>
    <strong>Author Name 1</strong><sup>1</sup>, 
    <strong>Author Name 2</strong><sup>1</sup>, 
    <strong>Author Name 3</strong><sup>2</sup>
  </p>

  <p>
    <sup>1</sup>Affiliation One &nbsp;&nbsp; 
  </p>

  <a href="https://arxiv.org/abs/2509.13816">
    <img src="https://img.shields.io/badge/Paper-ArXiv-B31B1B?style=for-the-badge&logo=arxiv&logoColor=white" alt="Paper">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Paper-PDF-red?style=for-the-badge&logo=adobeacrobatreader&logoColor=white" alt="PDF">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Code-GitHub-black?style=for-the-badge&logo=github&logoColor=white" alt="Code">
  </a>
  <a href="#">
    <img src="https://img.shields.io/badge/Video-YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Video">
  </a>

</div>

<br>

<div align="center">
  <img src="assets/teaser.gif" width="90%" alt="Drone navigating in forest">
  <p><em>Figure 1: Zero-shot sim-to-real flight in a dense forest. Our asynchronous policy enables agile navigation even with significant sensor delays.</em></p>
</div>

---

### 🟢 Abstract

Robust autonomous navigation for Autonomous Aerial Vehicles (AAVs) in complex environments is a critical capability. However, modern end-to-end navigation faces a key challenge: the high-frequency control loop needed for agile flight conflicts with low-frequency perception streams. 

To resolve this, we propose an **asynchronous reinforcement learning framework** that decouples perception and control. This enables a high-frequency policy to act on the latest IMU state for immediate reactivity, while incorporating perception features asynchronously. To manage the resulting data staleness, we introduce a theoretically-grounded **Temporal Encoding Module (TEM)**, complemented by a two-stage curriculum that ensures stable and efficient training. 

Validated in extensive simulations, our method was successfully deployed in **zero-shot sim-to-real transfer** on an onboard NUC, where it sustains a **100 Hz control rate** and demonstrates robust, agile navigation in cluttered real-world environments.

---

### 🎥 Method Overview

<div align="center">
  <img src="assets/method_overview.png" width="95%" alt="Method Architecture">
  <p><em>Figure 2: The Asynchronous End-to-End Learning Framework.</em></p>
</div>

Our framework addresses the **Age of Information (AoI)** problem caused by the mismatch between fast IMU updates and slow LiDAR perception.

* **Asynchronous Architecture:** Decouples the perception loop (LiDAR processing) from the control loop (Policy Inference).
* **Pseudo-Image Perception:** Converts 3D LiDAR point clouds into a 2D spherical projection (Pseudo-Image) for efficient CNN processing.
* **Temporal Encoding Module (TEM):** Explicitly encodes the time delay ($\Delta t_{lidar}$) into the state vector, allowing the policy to compensate for partial observability caused by data staleness.

---

### 🚀 Experiments & Results

We compared our method against state-of-the-art baselines like **NavRL**, **YOPO**, and **EGO-Planner-v2**.

#### Robustness to Low Sensor Frequency (10 Hz)
Even when perception is limited to 10 Hz, our method maintains a **91.08% success rate**, significantly outperforming synchronous baselines which degrade severely under latency.

| Model | Success Rate (100Hz Ideal) | Success Rate (10Hz Real) | Performance Loss |
| :--- | :---: | :---: | :---: |
| NavRL [16] | 86.96% | 75.37% | 11.6% |
| YOPO [13] | 67.71% | 58.51% | 9.2% |
| **Ours (Async)** | **93.67%** | **91.08%** | **2.6%** |

*(Data sourced from Table I of the paper)*

#### Real-World Deployment
The policy was deployed **zero-shot** on a custom quadrotor with a Livox Mid-360 LiDAR and Intel NUC 13.
* **Indoor Cluttered Field:** Successfully navigated dense obstacles ($0.25 m^{-2}$).
* **Outdoor Forest:** Demonstrated robust flight in unstructured environments ($0.18 m^{-2}$).

---

### 📝 Citation

```bibtex
@article{AgileDelay2026,
  title={Agile in the Face of Delay: Asynchronous End-to-End Learning for Real-World Aerial Navigation},
  author={Anonymous Author(s)},
  journal={arXiv preprint arXiv:2509.13816},
  year={2026}
}
