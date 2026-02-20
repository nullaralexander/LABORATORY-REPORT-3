# EXPERIMENT 17: Binary Phase Shift Keying

---

# I. INTRODUCTION
Building on the principles of ASK and FSK, Binary Phase Shift Keying (BPSK) offers a third method for transmitting digital data by using logic 1s and 0s to switch a carrier between two distinct phases. In a BPSK system, transitions in the digital message cause the carrier to shift its phase by 180°, effectively reversing the signal's direction—for instance, from a positive-bound peak toward a negative peak—whenever a logic level change occurs. Because the envelope of a BPSK signal mirrors the message shape in a way that identifies it as Double-Sideband Suppressed Carrier (DSBSC) modulation, it can be generated and demodulated using standard DSBSC techniques. While BPSK is mathematically the most robust against noise and produces the fewest errors compared to ASK and FSK, it is often more complex to implement, leading to the use of FSK or ASK in cost-sensitive applications like early dial-up modems. In this experiment, the Multiplier module will be used to implement the mathematical model for BPSK generation, followed by a second Multiplier for data recovery and a comparator to restore the final digital bitstream.

---

# II. OBJECTIVE
The objective of Experiment 17 is to investigate the principles of Binary Phase Shift Keying (BPSK) as a highly efficient method for digital data transmission. Specifically, the experiment aims to:
*	Implement the generation of a BPSK signal by using a Multiplier module to switch the phase of a carrier wave by 180° in response to the logic levels of a digital message.
*	Analyze the characteristics of the BPSK waveform to understand how it functions as a form of Double-Sideband Suppressed Carrier (DSBSC) modulation.
*	Demonstrate a demodulation technique using a second Multiplier module to recover the original data stream from the phase-shifted carrier.
*	Evaluate the signal restoration process by using a comparator to convert distorted, recovered data back into a clean digital bitstream.
*	Compare the performance of BPSK against ASK and FSK to understand why it is the superior system for noise immunity and error reduction.
*	
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

# 1. PART A – Generating a BPSK Signal
To initiate the generation of a Binary Phase Shift Keying (BPSK) signal, the oscilloscope is configured for high-fidelity viewing by setting the Trigger Source to EXT with HF REJ coupling and both input channels to DC coupling. Using a 0.1ms/div timebase, the Sequence Generator is set with dip-switches at 00 to model the digital message, while its SYNC output provides the stable trigger needed for the display. The Multiplier module then generates the BPSK signal by implementing the mathematical model of the carrier and data. By switching the scope to DUAL mode and activating Sweep Magnification, the user can closely compare the digital signal and the BPSK output, using the horizontal position control to observe the exact points where transitions occur. Finally, by deactivating the magnification and overlaying the digital signal with the BPSK signal's envelopes, the direct relationship between the binary logic levels and the resulting phase shifts can be visually verified.

## 1.1 Experiment Circuit Procedure
The Sequence Generator module serves to model the digital data stream, utilizing its SYNC output to trigger the oscilloscope for a consistent and stable visual display. Simultaneously, the Multiplier module generates the BPSK signal by implementing the specific mathematical model required to shift the carrier's phase in response to the digital input.

<img width="547" height="283" alt="P1" src="https://github.com/user-attachments/assets/bf0f9a4e-cba7-4708-90dd-f024c3bc456b" />

<img width="423" height="273" alt="P2" src="https://github.com/user-attachments/assets/cd8f0c3e-78c6-498d-a75a-04ed46b7300b" />

## OBSERVATION

![F1](https://github.com/user-attachments/assets/814e7056-e1c6-4b76-9640-ff281f9b8a30)

The oscilloscope capture demonstrates the successful generation of a Binary Phase Shift Keying (BPSK) signal through the mathematical multiplication of a carrier and a digital message. The red trace represents the digital data, while the yellow trace displays the modulated carrier wave, which maintains a constant frequency of approximately 13.93 kHz. A close inspection of the waveform at the bit transitions reveals the characteristic 180° phase reversals; specifically, when the digital signal shifts logic levels, the carrier wave immediately reverses its direction, confirming that the phase is being toggled between two states. By overlaying the two traces, it is evident that these phase shifts are perfectly coincident with the rising and falling edges of the digital pulse. This observation validates that the information is encoded entirely within the carrier's phase, resulting in a Double-Sideband Suppressed Carrier (DSBSC) signal that is highly resistant to noise.

# 2. PART B – Demodulating a BPSK signal using a product detector
To implement the demodulation of the BPSK signal, a product detector is constructed using a second Multiplier module in conjunction with the Tuneable Low-pass Filter (LPF). Since BPSK is mathematically equivalent to Double-Sideband Suppressed Carrier (DSBSC) modulation with a digital message, this conventional recovery scheme is highly effective for extracting the original data. The procedure begins by adjusting the Tuneable LPF module, ensuring the Cut-off Frequency control is turned fully clockwise while the Gain control is positioned at the midpoint of its travel. This configuration allows the product detector to process the BPSK signal and successfully isolate the baseband digital information from the high-frequency carrier components.

## 2.1 Experiment Circuit Procedure

<img width="618" height="252" alt="P3" src="https://github.com/user-attachments/assets/ab8c26b7-c76e-40bb-ba27-0937e8ead43a" />

<img width="645" height="334" alt="P4" src="https://github.com/user-attachments/assets/e000aa5a-b6c6-4054-b789-57b4e2d39cde" />

## OBSERVATION

![F2](https://github.com/user-attachments/assets/2d2547fe-7c40-4cd1-a20f-a987913200c2)

The observation of the BPSK demodulation process confirms that a product detector effectively extracts the baseband data from the phase-shifted carrier. As shown in the oscilloscope display, the red trace represents the original digital message, while the yellow trace displays the output from the Tuneable LPF. While the product detector has successfully recovered the logic levels of the digital bitstream, the resulting yellow waveform is rounded and exhibits significant "ringing" or ripples on the top and bottom of the pulses. This distortion occurs because the low-pass filter, while necessary to remove the high-frequency carrier components isolated by the second Multiplier, also attenuates the higher harmonics required to maintain the sharp, rectangular edges of the original digital signal. Consequently, the recovered data appears as a smoothed, analog-like representation of the binary sequence that will require further processing to restore its original digital integrity.

# 3. PART C- Encoding and decoding speech
Building on the principles established in Experiment 14, a comparator is employed in this final stage to effectively "clean up" the distorted digital signals resulting from the demodulation process. To initiate the restoration of the BPSK signal, the Variable DCV module's control is initially set to approximately the middle of its travel to provide a reference threshold. By comparing the original digital message to the recovered output, the Variable DC voltage is finely adjusted until the two signals are identical, successfully removing the rounding and ripples introduced during filtering to restore sharp, rectangular transitions.

## 3.1 Experiment Circuit Procedure


<img width="1125" height="435" alt="image" src="https://github.com/user-attachments/assets/2814ce5e-99e8-42b7-9002-0f1e30681e19" />

<img width="1125" height="441" alt="image" src="https://github.com/user-attachments/assets/0fbf95bc-e0c8-4bd7-99b8-3ca5ef2826a5" />

# OBSERVATION

![F3](https://github.com/user-attachments/assets/facc7294-a232-4c85-88ae-6a152e949d98)

The provided oscilloscope capture illustrates the successful final stage of signal recovery, where the original digital data is compared against the restored output. The red trace on Channel 1 represents the original digital message from the Sequence Generator, while the yellow trace on Channel 2 displays the "cleaned-up" output from the comparator. By processing the rounded, demodulated signal through the comparator against a set reference threshold, the system has effectively regenerated the sharp, vertical rising and falling edges characteristic of a high-fidelity square wave.
The visual alignment and matching frequency of 2.500 kHz on both channels confirm that the restoration process has eliminated the distortions and rounding introduced by the envelope detector's filtering. This observation demonstrates that despite the intermediary losses during transmission and demodulation, the use of a high-gain switching device can perfectly recover the digital integrity of the ASK message, resulting in a rectangular waveform with clear logic high and low levels.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What happens to the BPSK signal on the data stream's logic transitions?**

Answer: At the exact point where the digital data transitions between logic levels, the BPSK signal undergoes a 180° phase shift. This causes the carrier wave to immediately reverse its direction—for example, switching from heading toward a positive peak to heading toward a negative peak.

**Question 2: What feature of the BPSK signal suggests that it's a DSBSC signal?**

Answer: The BPSK signal is identified as a Double-Sideband Suppressed Carrier (DSBSC) signal because alternating halves of its envelopes share the same shape as the original digital message. This characteristic allows BPSK to be generated and recovered using conventional DSBSC modulation and demodulation techniques.

**Question 3: Why is the recovered digital signal not a perfect copy of the original?**

Answer: The recovered signal is not a perfect copy because the low-pass filtering required during the demodulation process removes the high-frequency harmonics of the digital pulse. This results in a waveform that is rounded, lacks sharp vertical edges, and may contain "ringing" or ripples.

**Question 4: What can be used to "clean-up" the recovered digital signal?**

Answer: A comparator is used to clean up and restore the distorted digital signal back to its original rectangular state.

**Question 5: Why does varying the DC voltage on the comparator's input change the shape of the digital signal?**

Answer: Varying the DC voltage changes the threshold level at which the comparator switches its output state. Because the recovered signal has slow-rising (sloped) edges rather than vertical ones, changing the reference voltage alters the exact moment the input crosses the threshold, thereby adjusting the width and timing of the restored pulses to match the original data.

---

# VI. Conclusion
Our exploration of the Binary Phase Shift Keying (BPSK) experiment successfully demonstrated the principles of phase-based digital modulation and the robust recovery stages required for high-fidelity data transmission. Using the Emona Telecoms-Trainer 101, we validated that digital information can be effectively encoded by toggling carrier phases and reconstructed using synchronous detection and threshold-based restoration.
*	Modulation and Phase Reversal: We proved that digital data can be superimposed onto a carrier by implementing a mathematical multiplication model, resulting in a constant-frequency signal that undergoes distinct 180° phase shifts at every logic transition. This established BPSK as a form of Double-Sideband Suppressed Carrier (DSBSC) modulation, where the information is stored entirely in the carrier's phase reversals.
*	Synchronous Demodulation and Filtering: We confirmed that a product detector, consisting of a second multiplier and a Tuneable Low-pass Filter, is highly effective for extracting the baseband digital message. However, we observed that the filtering necessary to remove high-frequency components inherently introduces rounding and "ringing" distortion, as the filter attenuates the harmonics required to maintain sharp rectangular edges.
*	Signal Restoration via Comparator: Our investigation into the restoration stage highlighted the essential role of the Voltage Comparator in overcoming analog degradation. By comparing the rounded, demodulated signal against a Variable DC reference threshold, we leveraged high-gain switching to regenerate sharp, vertical edges, effectively "cleaning up" the signal back to its original digital state.
*	System Integrity and Robustness: Finally, the perfect alignment between the original data and the restored 2.500 kHz output demonstrated that BPSK is a superior system for maintaining data integrity. While the intermediary analog stages introduce rounding and ripples, the use of threshold-based logic allows for the near-perfect reconstruction of the digital sequence, reinforcing BPSK's reputation as the best-performing system for ignoring noise and reducing errors.












