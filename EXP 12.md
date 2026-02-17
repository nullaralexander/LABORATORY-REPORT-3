# EXPERIMENT 11: Sampling and Reconstruction

---

# I. INTRODUCTION
Pulse Code Modulation (PCM) is a digital transmission system used to convert analog message signals into a serial stream of 0s and 1s. This conversion, known as encoding, is essential in modern telecommunications as digital systems continue to replace analog ones. The process involves sampling the analog signal at regular intervals, comparing these samples to reference quantization levels, and generating corresponding binary numbers. Key factors in PCM performance include the encoder's clock frequency, which must be at least twice the message frequency to avoid aliasing, and quantization error, which occurs because most sampled voltages do not exactly match a quantization level.

---

# II. OBJECTIVE
In this experiment, you will use the Emona Telecoms-Trainer 101 to:

*	To use the PCM Encoder module to convert fixed DC, variable DC, and continuously changing signals into PCM data.
*	To verify the operation of PCM encoding.
*	To investigate the concept of quantization error.


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

## 1. PART A – Introduction to PCM Encoding using a Static DC Voltage

## 1.1 Experiment Circuit Procedure
The PCM Encoder was clocked by an 8kHz digital output from the Master Signals module while the analog input was held at 0V DC. By viewing the Frame Synchronisation (FS) signal on the oscilloscope, we were able to identify the precise start and end of the digital data frames.

<img width="600" height="297" alt="Screenshot 2026-02-17 233532" src="https://github.com/user-attachments/assets/d62ec815-2543-4d45-a8b3-63d6ee2c4be5" />
<img width="398" height="293" alt="Screenshot 2026-02-17 233546" src="https://github.com/user-attachments/assets/a1cbaa04-d02a-4147-8372-291936c17d36" />


## OBSERVATION

![e12 1 1](https://github.com/user-attachments/assets/ae7a9c42-f291-4dff-88bd-52f7400f2a87)

During the observation of the PCM output for Part A, it was noted that when the input is held at a constant 0V DC, the encoder generates a stable and repeating 8-bit digital word. By using the Frame Synchronization (FS) signal as a trigger, we clearly identified the boundaries of each data packet, observing that the system transmits exactly one 8-bit frame per sampling period. A key finding was the bit-priority sequence: the encoder follows a "Most Significant Bit first" protocol, outputting bit-7 at the start of the frame followed by the remaining bits down to bit-0. The presence of 10 bits on the oscilloscope—representing one full frame and the beginning of the next—confirmed that the 8kHz clock successfully maintains a continuous and synchronized serial data stream.  

## 1.2 Experiment Circuit Procedure
Channel 2 should now display 10 bits of the PCM Encoder module's data output. The first 8 bits belong to one frame and the last two bits belong to the next frame.

<img width="687" height="324" alt="Screenshot 2026-02-17 234509" src="https://github.com/user-attachments/assets/e0953a6f-e074-4b13-a6a8-5c05af03ad65" />
<img width="465" height="331" alt="Screenshot 2026-02-17 234519" src="https://github.com/user-attachments/assets/ae47e2ff-3bf2-4d80-ac3b-cc2508510172" />

## OBSERVATION

![e12 1 2](https://github.com/user-attachments/assets/b0455b70-7853-49e7-b382-1ab23a4b13ef)

During the observation of the PCM output for Part 1.2, it was noted that the oscilloscope successfully displayed 10 bits of data: a complete 8-bit frame followed by the first two bits of the subsequent frame. This confirmed that the encoder operates on a continuous cycle, partitioning the analog input into discrete digital "words" at every clock pulse. We observed that the data is transmitted in a serial format where bit-7 (the Most Significant Bit) leads the frame, followed by bits 6 through 0. The stability of the 10-bit pattern while the input remained at 0V verified that the 8kHz clock and the encoder are perfectly synchronized, ensuring that each sample is accurately captured and framed without data drift.  

## 2. PART B – PCM Encoding of a Variable DC Voltage

## 2.1 Speech Sampling Procedure

#### Experiment Circuit Procedure
The Variable DCV module is used to let you change the Dc voltoge on the PcM Encode- module. input.The scope's external trigger input is used so that you can view ithe DC valtage on its Channel I input as a stable display.

<img width="749" height="352" alt="Screenshot 2026-02-18 003143" src="https://github.com/user-attachments/assets/e4c30ab7-2843-4fdd-9120-55cdae064875" />

<img width="564" height="383" alt="Screenshot 2026-02-18 003209" src="https://github.com/user-attachments/assets/6ad0246a-7c4f-4ad2-9f21-c73b4f9c8259" />

## OBSERVATION

![e12 2 1](https://github.com/user-attachments/assets/b833dfd9-7ead-4728-b78f-cfbc8247a9e2)

As we adjusted the variable DC control, we observed how the encoder dynamically generated different 8-bit binary output codes in response to the changing analog input levels. Moving the DC voltage above and below the reference line caused the serial bit pattern to shift, demonstrating the real-time quantization process. Final measurements confirmed the accuracy of the system, as the input voltage was recorded to be very close to 0V when the encoder produced the specific binary code previously identified during the static 0V test.  

## 3. PART D- PCM Encoding  of Continously changing voltages

## 3.1 Experiment Circuit Procedure
We will be using the PCM Encoder module to convert continuously changing signals, specifically a sinewave, into a digital bitstream. Our goal is to observe how the encoder handles dynamic analog data by using a high-frequency 50kHz clock from the VCO module, allowing us to visualize the rapid transition of binary codes as the input signal fluctuates over time.  

<img width="644" height="272" alt="Screenshot 2026-02-17 235707" src="https://github.com/user-attachments/assets/0c0c12ed-e5db-4c62-8013-2a179cacf0eb" />

## OBSERVATION

![e12 4 1](https://github.com/user-attachments/assets/5c2f06e3-b20d-41b2-950b-9a5ad23ed836)

In this stage of the experiment, the PCM Encoder module was used to digitize a continuously changing 2kHz sine wave signal. To ensure accurate sampling of the dynamic waveform, a high-speed 50kHz clock from the VCO module was implemented, providing a sampling rate well above the Nyquist requirement. Observation of the PCM data output on the oscilloscope revealed a "dancing" or rapidly shifting bit pattern, which represents the encoder’s real-time process of updating the 8-bit binary codes to match the fluctuating instantaneous voltage of the sine wave. Despite the constant variation in the data bits, the Frame Synchronization (FS) signal remained stable, confirming that the encoder successfully maintains a rigid 8-bit framing structure even when processing complex, time-varying analog information.  

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: Indicate on your drawing the start and end of the frame.**

Answer: A frame begins with bit-7 (the most significant bit) and ends after bit-0 (the least significant bit). The Frame Synchronisation (FS) signal can be used to identify these boundaries, as it goes high at the same time bit-0 is outputted.

**Question 2: Indicate on your drawing the start and end of each bit.**

Answer: Each bit is defined by the PCM clock; one bit is outputted for every clock cycle.

**Question 3: Indicate on your drawing which bit is bit-0 and which is bit-7.**

Answer: Bit-7 is the most significant bit and is sent first in the frame. Bit-0 is the least significant bit and is sent last, occurring at the same time the FS signal goes high.

**Question 4: What is the binary number that the PCM Encoder module is outputting?**

Answer: This is determined by observing the sequence of 1s and 0s on the oscilloscope. For a 0V DC input, the specific 8-bit code is a result of the module's internal quantization.

**Question 5: Why does the code change even though the input voltage is steady?**

Answer: The code may flicker between adjacent quantization levels because of quantization error or small amounts of noise on the steady DC input, which causes the encoder to alternate between two nearby digital representations

**Question 6: Why does the PCM Encoder module output this code for 0V DC and not 00000000?**

Answer: The PCM Encoder (codec) is designed to convert analog voltages between -2V and +2V into 256 levels (0 to 255). In such a bipolar system, 0V is typically represented by a mid-range code (around 128 or 10000000) rather than all zeros, which would represent the most negative voltage (-2V).

**Question 7: What happens to the Variable DCV module's output?**

Answer: As you adjust the control, the DC voltage level increases or decreases relative to the zero-volt reference line.

**Question 8: In what way does the binary number that the PCM Encoder module outputs change?**

Answer: As the input voltage changes, the 8-bit binary pattern shifts to different values to represent the new quantization level closest to the new analog voltage.

**Question 9: What happens to the Variable DCV module's output?**

Answer: (This refers to further adjustment in the procedure) The output voltage continues to vary linearly according to the position of the variable control knob.

**Question 10: What happens to the binary number that the PCM Encoder module is outputting?**

Answer: The binary number continues to update in real-time to match the closest quantization level for the current input voltage.

**Question 11: Based on the information in Table 1, what is the maximum allowable amplitude (peak-to-peak) for an AC signal on the PCM Encoder module's INPUT?**

Answer: The encoder is designed for voltages between -2V and +2V. Therefore, the maximum allowable peak-to-peak amplitude is 4Vpp.

**Question 12: What's the name for the difference between a sampled voltage and its closest quantisation level?**

Answer:  This difference is known as quantisation error.

**Question 13: Calculate the difference between the quantisation levels in the PCM Encoder module by subtracting the values in Table 1 and dividing the number by 256.**

Answer: 
The range is 4V (-2V to +2V). Dividing this total range by the 256 possible codes (2^8 bits) gives a resolution of approximately 15.6 mV per level (4V / 256 ≈0.0156V).

**Question 14: To reduce quantisation error it's better to have:**

Answer: **more quantisation levels between ±2V.** (The more levels there are, the closer they are together, which reduces the difference between the sample and the nearest level) .

**Question 15: Why does the PCM DATA change continuously?**

Answer: When the input is a continuously changing signal (like a sine wave), the voltage is at a different level for every sample. Consequently, the encoder must generate a different binary code for every frame to represent the signal's changing value.

---

# VI. Conclusion

The experiment successfully demonstrated the principles and operation of Pulse Code Modulation (PCM) using the Emona Telecoms-Trainer 101. By progressing from static DC voltages to dynamic sine waves, we verified that the PCM encoding process effectively converts analog signals into a structured serial stream of binary data.

* **Framing and Synchronization:** We confirmed that the encoder organizes data into discrete 8-bit frames. The use of the Frame Synchronization (FS) signal was proven essential for identifying the start of each data packet, ensuring that the receiver can distinguish between individual samples in a continuous bitstream.
  
* **Bit Protocol:** Observations across all parts of the experiment identified a consistent "Most Significant Bit (MSB) first" transmission protocol. By identifying bit-7 as the leading bit, we established how the system maintains numerical integrity during serial transmission.
  
*	**Quantization Accuracy:** Through the use of variable DC voltages, the experiment illustrated the relationship between analog levels and their digital equivalents. The system showed high precision, as evidenced by the binary output for 0V consistently matching the theoretical expectations.
  
*	**Dynamic Signal Handling:** The transition to a continuously changing sine wave demonstrated the importance of the sampling rate. By utilizing a high-frequency 50kHz clock, the encoder was able to accurately track and digitize rapid voltage fluctuations, resulting in a dynamic "dancing" bit pattern that maintained its 8-bit frame integrity despite the complexity of the input.
  
In conclusion, the experiment provided a comprehensive understanding of the fundamental stages of PCM—sampling, quantization, and encoding. We successfully validated that as long as synchronization is maintained and the sampling frequency satisfies the Nyquist requirement, any analog signal can be accurately represented and transmitted as a digital serial bitstream.
