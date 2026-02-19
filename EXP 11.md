# EXPERIMENT 11: Sampling and Reconstruction

---

# I. INTRODUCTION
In this session, we transition from purely analog systems to the foundational processes that make modern digital communication possible. Digital transmission has largely superseded analog due to its superior resistance to electrical noise and interference. However, since most real-world data—such as speech or music—is inherently analog, we must first "translate" these continuous signals into a format that digital systems can process. This bridge is built through a process called **sampling**.

### Understanding the Sampling Process
Sampling involves measuring the voltage of an analog "message" signal at precise, regular intervals. This experiment explores two primary methods of capturing these measurements:

1.  **Natural Sampling:** The sampled signal follows the exact shape of the message during the brief window that the sampling gate is open. If the message voltage changes during that window, the sample reflects that change.
2.  **Sample-and-Hold / Pulse Amplitude Modulation (PAM):** To create a more stable signal for certain digital systems, the voltage is "frozen" at the exact moment of measurement, creating a series of flat-topped pulses.

### The Mathematics of Recovery
A critical question in digital theory is how we can possibly recover a smooth, continuous message from a series of disconnected pulses. The answer lies in the mathematical relationship:

$$\text{Sampled Message} = \text{Sampling Signal} \times \text{Message}$$

Because a digital sampling signal is actually a composite of a DC voltage, a fundamental frequency, and multiple harmonics, the resulting sampled signal contains a "ghost" of the original message at its original frequency. By passing this complex mixture through a **Low-Pass Filter (LPF)**, we can strip away the high-frequency harmonics and isolate the original analog signal.

---

# II. OBJECTIVE
In this experiment, you will use the Emona Telecoms-Trainer 101 to:

* **Implement and compare** Natural Sampling and Sample-and-Hold schemes.
* **Demonstrate the reconstruction** of an analog message from its sampled version using filtering.
* **Investigate the "catch"** mentioned in the theory—the phenomenon of aliasing—and determine what happens when the sampling rate is too low.
  
---

# III. MATERIALS

| Item | Description |
| :--- | :--- |
| **Trainer Unit** | Emona Telecoms-Trainer 101 (plus power-pack) |
| **Oscilloscope** | Dual channel 20MHz oscilloscope |
| **Leads (Scope)** | Two Emona Telecoms-Trainer 101 oscilloscope leads |
| **Leads (Patch)** | Assorted Emona Telecoms-Trainer 101 patch leads |

---

# IV. EXPERIMENTAL RESULTS

# 1. PART A – Sampling a Simple Message
For this stage of our experiment, we utilized the **Dual Analog Switch module** on the Emona Telecoms-Trainer 101. The objective was to sample a simple message signal using two distinct techniques: **Natural Sampling** and **Sample-and-Hold**.

## 1.1 Natural Sampling Technique
#### Experiment Circuit Procedure
The setup uses an electronically controlled switch to connect the message signal (the **2kHz SINE** output from the Master Signals module) to the output. The switch is opened and closed by the **8kHz DIGITAL** output of the Master Signals module.

<img width="552" height="335" alt="Screenshot 2026-02-17 210931" src="https://github.com/user-attachments/assets/4a3b165b-b71d-47d3-bff5-b8273633db48" />

<img width="490" height="312" alt="Screenshot 2026-02-17 211153" src="https://github.com/user-attachments/assets/b6b07a4d-b96e-4c4a-89aa-c509852409e1" />

## OBSERVATION

![1](https://github.com/user-attachments/assets/2150461b-7f6e-40c4-b2d9-fe7d25155382)

The red trace on the oscilloscope represents our original analog message, while the dense yellow area represents the sampled output created by the high-speed switching process. Because sampling is mathematically the multiplication of the message and the sampling signal, we can see the yellow pulses "tracking" the shape of the red sinewave, effectively using the message as an envelope. This specific visual result confirms the "natural" sampling technique, where the voltage of the pulses continues to change along with the message signal for the duration that the sampling gate remains open.

## 1.2 Sample-and-Hold / Pulse Amplitude Modulation (PAM)
#### Experiment Circuit Procedure
The electronically controlled switch in the original setup was substituted for a **Sample-and-Hold circuit**. The message and sampling signals remained constant:
* **Message:** 2kHz Sinewave
* **Sampling Signal:** 8kHz Pulse Train
  
<img width="522" height="302" alt="Screenshot 2026-02-17 211908" src="https://github.com/user-attachments/assets/f00be9a5-007c-48f8-9875-ff1e4acb90e6" />

<img width="505" height="336" alt="Screenshot 2026-02-17 211859" src="https://github.com/user-attachments/assets/60adbb62-1231-4800-b568-371933be088c" />

## OBSERVATION

![2](https://github.com/user-attachments/assets/23b30cd4-d545-491c-b7a0-3a3dde7be5bb)

In this stage of our experiment, we swapped the basic switch for a sample-and-hold circuit. While our signals stayed the same—a 2kHz sinewave message and an 8kHz sampling pulse—the output changed significantly.
Instead of following the smooth curve of the sinewave, the yellow sampled signal now looks like a staircase. This happens because the circuit grabs the message’s voltage at the start of each pulse and "freezes" it, creating flat-topped pulses instead of curved ones. This process is known as Pulse Amplitude Modulation (PAM), and it is essential for digital systems that need a steady, unchanging voltage to process data accurately.

# 2. PART B – Sampling Speech
While previous stages focused on a 2kHz sinewave, commercial digital communications systems primarily handle complex data like speech and music. This part of the experiment demonstrates the behavior of a sampled speech signal.

## 2.1 Speech Sampling Procedure

#### Experiment Circuit Procedure
The 2kHz Sine wave was replaced by the **Speech module** output of the Emona Telecoms-Trainer 101. The sampling parameters (8kHz pulse train) remained constant to observe how the system handles non-periodic, real-world signals.

<img width="648" height="343" alt="Screenshot 2026-02-17 212253" src="https://github.com/user-attachments/assets/d66f7900-23da-4373-804c-8ef1f2958f5a" />


## OBSERVATION

![3 1](https://github.com/user-attachments/assets/68143d7e-db12-4d73-8bcf-73f44c29a5c0)
![3 2](https://github.com/user-attachments/assets/a0fa48e4-7180-4fc8-a5d2-00a5be10dcbc)

In this phase of our experiment, we transitioned from a simple 2kHz sinewave to a complex, real-world signal by connecting the Speech module output. While the sampling parameters remained constant, the oscilloscope now displays highly dynamic red traces that represent the irregular and varying frequencies of human speech or humming. As we observe the yellow sampled signal, we can see it continues to track the voice input using the sample-and-hold method, creating a "staircase" of flat-topped pulses that shift in real-time to match the pitch and volume of our voice. This demonstrates that the same sampling principles used for basic waves are effective for capturing the intricate data required for commercial digital communication systems.


# 3. PART C – Reconstructing a Sampled Message
A sampled message is a composite of many sinewaves. Crucially, for every sinewave in the original message, there is a corresponding sinewave in the sampled signal at that same frequency. 

**Reconstruction** involves passing the sampled signal through a **Low-Pass Filter (LPF)**. This allows the original message frequencies to pass while rejecting the high-frequency sampling harmonics.


## 3.1 Experiment Circuit Procedure
For this stage, we utilized the **Tuneable Low-pass Filter module**. This module allows us to manually adjust the **cut-off frequency** (the point at which frequencies are rejected) using the "Cut-off Frequency Adjust" control.

<img width="642" height="300" alt="Screenshot 2026-02-17 212950" src="https://github.com/user-attachments/assets/c1868908-b127-435c-a384-e4f0294259df" />

<img width="692" height="441" alt="Screenshot 2026-02-17 213012" src="https://github.com/user-attachments/assets/6a07208a-7093-4cd9-9ccd-b2e81f9b9354" />

## OBSERVATION

![partc 1](https://github.com/user-attachments/assets/acc24586-d6ec-4aa0-b32f-e48582f3473a)

Filter at Cut-off (Minimum Frequency)
When the Cut-off Frequency Adjust control is turned fully counter-clockwise, the filter rejects almost all frequencies, including the message. As seen in the oscilloscope, while the original red message signal remains visible, the yellow output from the filter is a flat line, indicating that no signal is being passed through.

![partc 2](https://github.com/user-attachments/assets/042aa1a4-259f-4a6e-9434-c3da52e021ac)

Fully Reconstructed Signal
As we turn the control clockwise, we increase the cut-off frequency until the message signal is allowed to pass. In the second oscilloscope, the yellow trace has transformed into a smooth sinewave that closely matches the red original message.


# 4. PART D – Aliasing
In this final section, we investigate **aliasing**, a critical form of distortion that occurs when the sampling frequency is too low to accurately capture the message. Successful reconstruction is only possible when the sampling rate is high enough to keep unwanted frequency components—the aliases—outside the range of the filter.

## 4.1 Experiment Circuit Procedure
The fixed 8kHz sampling signal was replaced with a signal from the **VCO (Voltage Controlled Oscillator) module**, allowing for a manually adjustable sampling frequency.

<img width="757" height="308" alt="Screenshot 2026-02-17 213939" src="https://github.com/user-attachments/assets/49a4a41a-b349-4dbd-a6d3-8c030277300b" />

<img width="691" height="443" alt="Screenshot 2026-02-17 214108" src="https://github.com/user-attachments/assets/a67e119e-744f-4be4-ac4d-b72d567cb2bb" />

## OBSERVATION

In this final stage of our experiment, we explored the phenomenon of aliasing by replacing the fixed 8kHz sampling signal with a manually adjustable frequency from the VCO module. As we lowered the sampling frequency toward the Nyquist Sample Rate (twice the message frequency, or 4kHz for our 2kHz sinewave), we observed significant distortion in the reconstructed output. This occurs because the "aliases"—unwanted frequency components created by the sum and difference of the sampling and message frequencies—begin to drop low enough to pass through our Tuneable Low-pass Filter. Even though the theoretical minimum rate is 4kHz, we noted that real-world filters are not perfect and require a sampling rate slightly higher than this threshold to effectively reject these overlapping signals. Our observations confirm that failing to maintain an adequate sampling rate causes these aliases to merge with the original message, making it impossible to reconstruct a clean analog signal.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What type of sampling is this an example of?**

Answer: This was an example of Natural Sampling.


**Question 2: What two features of the sampled signal confirm this?**

Answer:
1. **Changing Sample Voltages:** We observed that the voltage of each sample continued to change and follow the message's curve while the sampling gate was open.
2. **Return to Zero:** The signal consistently dropped back to zero volts during the intervals between each sample.


**Question 3: What two features of the sampled signal confirm that the set-up models the sample-and-hold scheme?**

Answer:
1. **Static Sample Voltages:** Unlike natural sampling, the voltage levels remained perfectly flat (frozen) for the entire duration of the sample.
2. **No Inter-sample Gaps:** There were no gaps or returns to zero between the samples, creating a continuous "staircase" effect.


**Question 4: What’s the name of the distortion that appears when the VCO module’s Frequency Adjust control is turned far enough?**

Answer: This distortion is known as Aliasing.

**Question 5: Given the message is a 2kHz sinewave, what’s the theoretical minimum frequency for the sampling signal?**

Answer: The theoretical minimum is 4kHz, calculated as twice the message frequency ($2 \times 2\text{kHz}$) according to the Nyquist Criterion.


 **Question 6: Why is the actual minimum sampling frequency higher than the theoretical minimum calculated in Question 5?**

Answer: This is necessary because real-world filters are not perfect. They have a gradual transition (roll-off) rather than an instantaneous "brick-wall" cut-off, requiring a wider frequency gap (guard band) to properly reject aliases.

---
 
# VI. Conclusion
Our exploration of Experiment 11 has successfully demonstrated the fundamental bridge between the analog and digital worlds. By using the Emona Telecoms-Trainer 101, we validated that continuous information—whether a simple sinewave or complex human speech—can be effectively captured, transmitted, and reconstructed through the process of sampling.

* **Sampling Techniques:** We proved that while **Natural Sampling** maintains the message's shape during the sampling interval, the **Sample-and-Hold** method provides the stabilized, flat-topped pulses (**Pulse Amplitude Modulation**) necessary for modern digital processing.
  
* **Message Recovery:** We confirmed the mathematical theory that a sampled signal contains the original message frequency. By utilizing a **Tuneable Low-pass Filter**, we successfully isolated this frequency, transforming discrete "staircase" pulses back into a smooth, recognizable analog wave.

* **The Importance of Sample Rate:** Our investigation into **Aliasing** highlighted the critical nature of the **Nyquist Sample Rate**. We observed that if the sampling frequency drops too close to (or below) twice the message frequency, unwanted "aliases" interfere with the reconstruction, causing permanent distortion.

* **Real-World Constraints:** Finally, we noted that while theory suggests a minimum sampling rate, practical limitations of hardware and filters require a slightly higher sampling rate to ensure a clean, high-fidelity reconstruction.

This experiment solidifies our understanding of why digital systems are so robust: by breaking a signal into discrete pieces, we gain resistance to noise, provided we respect the mathematical boundaries required to put those pieces back together.
