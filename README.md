# 📡 ECE Laboratory Experiments – Telecommunications Fundamentals

# 📘 Overview
This laboratory series traces the evolution of telecommunications from basic digitization to advanced transmission. It begins by establishing the "Digital Bridge," where Sampling and Pulse Code Modulation (PCM) are used to convert analog signals into binary data, emphasizing that reconstruction depends entirely on the Nyquist Criterion and precise synchronization.

The middle phase addresses real-world transmission challenges, such as Bandwidth Limiting and signal distortion. By implementing various modulation schemes—ASK, FSK, BPSK, and QPSK—the experiments demonstrate how digital information is superimposed onto carrier waves. This section highlights the shift from simple amplitude switching to phase-based modulation, which offers superior noise immunity and doubles data capacity through spectral efficiency.

The final experiments explore modern, secure systems and Software Defined Radio (SDR). Through Direct Sequence Spread Spectrum (DSSS), the sessions show how pseudo-noise sequences protect data from jamming, while Undersampling techniques prove that software-driven logic can perform direct frequency down-conversion. Ultimately, the series reinforces that modern communication relies on the mathematical precision of timing, filtering, and threshold-based restoration to maintain data integrity across any medium.

---

# 🧪 Experiments Included

### EXPERIMENT 11: Sampling and Reconstruction [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2011.md)
The transition from analog to digital begins with sampling, a process that measures an analog signal's voltage at regular intervals. This experiment explores two main techniques: Natural Sampling, where the sampled signal follows the exact shape of the message during the sampling window, and Sample-and-Hold, which freezes the voltage to create flat-topped pulses for better stability. Mathematically, the sampled signal contains a "ghost" of the original message at its base frequency. By passing this complex signal through a Low-Pass Filter, the high-frequency harmonics are removed, allowing the original continuous message to be reconstructed. 

### EXPERIMENT 12: PCM Encoding [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2012.md)
Pulse Code Modulation (PCM) is the standard for converting analog signals into a digital stream of 1s and 0s. The process involves sampling the message, comparing those samples to specific quantization levels, and assigning each level a binary number. A key constraint is the sampling clock frequency, which must be at least twice the message frequency to prevent aliasing. Because real-world voltages rarely match the fixed quantization levels perfectly, a small amount of detail is lost, resulting in an inherent distortion known as quantization error. 

### EXPERIMENT 13: PCM Decoding [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2013.md)
Decoding is the process of translating a serial bitstream back into a usable analog signal. The decoder must group the incoming bits into 8-bit frames and generate a proportional voltage for each, creating a Pulse Amplitude Modulation signal. This experiment emphasizes the absolute necessity of synchronization; since the system is not self-clocking, the decoder must "steal" the clock and frame synchronization signals from the encoder to accurately reconstruct the data. Once the voltages are generated, a low-pass filter smooths the pulses back into the original waveform.

### EXPERIMENT 14: Bandwidth Limiting and Restoring Digital Signals [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2014.md)
Every communication channel has a limited bandwidth that acts as a filter, removing the high-frequency components essential for sharp digital pulses. When a PCM signal travels through such a channel, the square waves become rounded and distorted, making it difficult for the receiver to distinguish between high and low logic levels. This experiment uses a low-pass filter to model this degradation and then introduces a comparator as a restoration tool. The comparator attempts to "square up" the signal, though its effectiveness is limited if the distortion is too severe.

### EXPERIMENT 15: Amplitude Shift Keying (ASK) [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2015.md)
Amplitude Shift Keying is a digital modulation technique where a high-frequency carrier wave is switched on or off to represent logic levels. It is essentially a digital version of AM broadcasting. While the signal is easy to recover using a simple envelope detector—which traces the "outer shell" of the waveform to find the data—it is highly susceptible to electrical noise that can change the carrier’s amplitude. To ensure a clean output, the recovered signal is often passed through a comparator to restore its original digital integrity.

### EXPERIMENT 16: Frequency Shift Keying (FSK) [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2016.md)
Frequency Shift Keying improves upon ASK by using two distinct frequencies to represent data: a lower "space" frequency for logic 0 and a higher "mark" frequency for logic 1. This method provides superior noise immunity because the receiver can use limiters to ignore amplitude spikes without losing the frequency-based information. In this experiment, a Voltage Controlled Oscillator (VCO) generates the FSK signal, and the data is recovered by filtering for specific frequency components followed by an envelope detector and a comparator.

### EXPERIMENT 17: Binary Phase Shift Keying (BPSK) [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2017.md)
Binary Phase Shift Keying transmits data by shifting the phase of a carrier wave by 180° whenever the logic level changes. This effectively reverses the signal's direction, making it a form of Double-Sideband Suppressed Carrier (DSBSC) modulation. While BPSK is mathematically the most robust against noise and produces the fewest transmission errors, it is more complex to implement than ASK or FSK. The experiment utilizes multipliers for both the modulation and the phase-sensitive recovery of the digital bitstream.

### EXPERIMENT 18: Quadrature Phase Shift Keying (QPSK) [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2018.md)
Quadrature Phase Shift Keying is a highly efficient modulation scheme that doubles the data capacity of a channel by transmitting two bits simultaneously. A bit-splitter divides the data into even and odd streams, which are then modulated onto two carriers that are 90° out of phase with each other. Because these signals are orthogonal, a product detector at the receiver can separate them without interference. This allows more users to share the same frequency spectrum without increasing the overall bandwidth required for the transmission.

### EXPERIMENT 19: DSSS Modulation and Demodulation [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2019.md)
Direct Sequence Spread Spectrum (DSSS) distributes message information across a very wide frequency range using a high-speed pseudo-noise (PN) sequence as a carrier. This "spreading" makes the signal incredibly resistant to jamming and deliberate interference, as the energy is spread so thin it may look like background noise. For successful recovery, the receiver must use an identical, synchronized PN sequence. This technology is fundamental to secure systems like GPS and modern Wi-Fi networks due to its inherent encryption and robustness.

### EXPERIMENT 20: Undersampling in SDR (Software Defined Radio) [click here](https://github.com/nullaralexander/LABORATORY-REPORT-3/blob/main/EXP%2020.md)
Software Defined Radio uses software to replace traditional hardware components, but processing high-frequency signals often requires impossible sampling rates. This experiment explores "undersampling" or band-pass sampling, which proves that if a signal is bandwidth-limited, it can be captured at a rate related to its bandwidth rather than its carrier frequency. When the undersampling rate is correctly matched, the process inherently demodulates the signal, allowing the original message to be recovered with a simple low-pass filter.

---

# 🎯 Learning Objectives
### Part 1: The Digital Bridge (Experiments 11 - 14)
 * Fundamental Digitization: Master the mechanics of Sampling (Natural vs. Sample-and-Hold) and the PCM Encoding process to convert continuous analog signals into 8-bit digital data.

 * Signal Reconstruction: Demonstrate how to successfully recover analog messages using Low-Pass Filtering and analyze the critical importance of Clock and Frame Synchronization.

 * Error & Distortion Analysis: Investigate physical limitations such as Aliasing (sampling too slowly), Quantization Error (rounding noise), and Bandwidth Limiting (channel distortion).

 * Signal Restoration: Implement hardware solutions like Comparators to "square up" and restore digital pulses that have been degraded by the transmission medium.

### Part 2: Digital Modulation (Experiments 15 - 18)
 * Carrier Modulation Techniques: Implement and compare three primary methods of shifting digital data onto high-frequency waves: Amplitude (ASK), Frequency (FSK), and Phase (BPSK).

 * Demodulation Strategies: Build recovery circuits using various methods, including Envelope Detectors for ASK/FSK and Product Detectors (Multipliers) for phase-sensitive BPSK.

 * Spectral Efficiency: Explore QPSK to understand how "bit-splitting" allows two independent data streams to occupy the same frequency space, doubling the capacity of the channel.

 * Performance Evaluation: Analyze the trade-offs between system complexity and Noise Immunity, identifying why phase modulation (BPSK/QPSK) is superior for minimizing transmission errors.

### Part 3: Advanced Transmission & SDR (Experiments 19 - 20)
 * Spread Spectrum Security: Model DSSS by using Pseudo-Noise (PN) sequences to "hide" data within wideband noise, making transmissions resistant to jamming and unauthorized interception.

 * Sequence Synchronization: Verify that successful DSSS recovery requires the receiver to match the transmitter’s code and phase exactly, highlighting the system's inherent encryption.

 * Software Defined Radio Principles: Challenge traditional Nyquist limits by implementing Undersampling (Band-pass sampling) to process high-frequency signals at much lower rates.

 * Efficient Down-Conversion: Validate Shannon’s Information Theorem by showing that the sampling process itself can perform frequency down-conversion and demodulation in a single step.

---

# 🛠️ Equipment Used
| Item | Description |
| :--- | :--- |
| **Trainer Unit** | Emona Telecoms-Trainer 101 (plus power-pack) |
| **Oscilloscope** | Dual channel 20MHz oscilloscope |
| **Leads (Scope)** | Two Emona Telecoms-Trainer 101 oscilloscope leads |
| **Leads (Scope)** | Three Emona Telecoms-Trainer 101 oscilloscope leads |
| **Leads (Patch)** | Assorted Emona Telecoms-Trainer 101 patch leads |
| **HeadPhone** | Stereo Headphones |

---
# 📔 Overall Laboratory Discussion & Reflection

## Part 1: The Digital Bridge (Experiments 11 - 14)
### Experiment 11 (Sampling and Reconstruction): 
This experiment validated the Nyquist-Shannon Theorem. We proved that analog signals can be converted into discrete pulses without loss of information, provided the sampling rate is sufficient. The use of a Low-Pass Filter (LPF) was essential to remove the high-frequency switching noise and reconstruct the smooth original wave.

### Experiment 12 (PCM Encoding): 
We explored the transformation of analog voltages into a structured 8-bit binary stream. A key observation was the "MSB-first" protocol and the necessity of Frame Synchronization (FS) to tell the receiver exactly where a new sample begins within the continuous bitstream.

### Experiment 13 (PCM Decoding): 
This session demonstrated that the immediate result of decoding is a "staircase" Pulse Amplitude Modulation (PAM) signal. While this signal contains the correct data, it requires filtering to smooth out quantization noise and sharp transitions, highlighting that reconstruction is a two-step process: decoding plus filtering.

### Experiment 14 (Bandwidth Limiting and Restoring): 
We modeled real-world channel limitations. By restricting bandwidth, we observed the "closing" of the Eye Diagram, which visually represents how intersymbol interference (ISI) makes it difficult to distinguish between 1s and 0s. We also proved that Comparators can restore pulse shapes but cannot fix the timing shifts introduced by the channel.

## Part 2: Digital Modulation (Experiments 15 - 18)
### Experiment 15 (Amplitude Shift Keying): 
We successfully modeled the simplest digital modulation (ON/OFF switching). We learned that while an Envelope Detector is a simple way to recover data, the process is highly dependent on carrier-to-bit-rate separation and requires a comparator to "square up" the resulting rounded signals.

### Experiment 16 (Frequency Shift Keying): 
By using a Voltage Controlled Oscillator (VCO) to switch between "Mark" and "Space" frequencies, we observed superior noise immunity. We also demonstrated a creative demodulation method: using a filter to turn frequency shifts back into amplitude shifts (ASK) for easier detection.

### Experiment 17 (Binary Phase Shift Keying): 
This experiment established BPSK as a highly robust modulation form. By flipping the carrier phase by 180°, we stored data in the phase transitions. While the recovery required complex Synchronous Demodulation (using multipliers), the resulting data integrity was far superior to ASK or FSK.

### Experiment 18 (Quadrature Phase Shift Keying): 
We explored spectral efficiency. By splitting the data into even and odd bits and modulating them onto carriers 90° apart, we proved that two separate signals can occupy the same frequency space simultaneously. This effectively doubles the capacity of a communication channel.

## Part 3: Advanced Transmission & SDR (Experiments 19 - 20)
### Experiment 19 (DSSS Modulation and Demodulation): 
We investigated Spread Spectrum technology. By multiplying the message with a high-speed Pseudo-Noise (PN) sequence, the signal becomes "hidden" in the noise floor. We demonstrated its incredible interference immunity, where even signals buried under 0dB of noise could be perfectly recovered through processing gain.

### Experiment 20 (Undersampling in SDR): 
This final experiment challenged the standard Nyquist rule. We proved that for bandwidth-limited signals, we can sample at a rate much lower than the carrier frequency (Undersampling). This allowed a Sample-and-Hold circuit to act as a direct down-converter, demonstrating the flexible, hardware-efficient architecture used in modern Software Defined Radios.


---

## 💡 Final Reflection

The collective journey through these experiments illustrates the fundamental evolution of telecommunications from basic signal digitization to the sophisticated modulation techniques that define modern wireless infrastructure. The initial phase established the "digital bridge," proving through sampling and Pulse Code Modulation that analog information—such as human speech—can be broken into discrete binary pieces and reconstructed with high fidelity, provided we respect mathematical boundaries like the Nyquist Criterion and maintain strict synchronization. We observed that while the physical world imposes constraints like bandwidth limiting and quantization noise, the inherent robustness of digital logic allows us to use tools like comparators and low-pass filters to restore signal integrity even after significant channel degradation.

As the curriculum progressed into digital modulation, the focus shifted from merely creating bits to efficiently transporting them across the radio frequency spectrum. By implementing ASK, FSK, and BPSK, we analyzed the critical trade-offs between hardware simplicity and noise immunity. The transition to QPSK provided a masterclass in spectral efficiency, demonstrating how phase-quadrature allows a system to double its data capacity without requiring additional bandwidth. These sessions highlighted that the "shape" of a signal is less important than its timing and phase, which are the true anchors of reliable data transmission in congested environments.

The final stage of the laboratory series pushed beyond traditional boundaries, exploring the security of Spread Spectrum technology and the flexibility of Software Defined Radio. We validated that by using pseudo-noise sequences in DSSS, a signal can be spread so thinly that it becomes indistinguishable from background noise, yet remains perfectly recoverable and resistant to jamming. Finally, the exploration of undersampling in SDR proved that modern communication is increasingly defined by software-based logic rather than rigid hardware. This shift allows for "super-Nyquist" processing that simplifies receiver architecture, ultimately reinforcing the conclusion that synchronization, mathematical precision, and filtered reconstruction are the three pillars that allow digital information to survive and thrive in a noisy analog world.
