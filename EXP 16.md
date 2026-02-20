# EXPERIMENT 16: Frequency Shift Keying
---

# I. INTRODUCTION
This experiment explores Frequency Shift Keying (FSK), a digital adaptation of frequency modulation (FM) used within Frequency Division Multiplexing (FDM) to enable efficient channel sharing. Unlike Amplitude Shift Keying, FSK offers superior noise immunity because FM receivers can utilize limiters to remove amplitude variations caused by noise without damaging the integrity of the recovered message. An FSK signal operates by switching between two distinct frequencies: a lower "space frequency" representing logic 0s and a higher "mark frequency" representing logic 1s. Throughout this procedure, a Voltage Controlled Oscillator (VCO) will be used to generate the FSK signal from a digital sequence, and the data will be recovered by filtering for a specific frequency component and applying an envelope detector. Finally, a comparator will be employed to "clean up" any resulting signal distortion and restore the original digital bitstream.

---

# II. OBJECTIVE
The objective of this experiment is to explore the principles of Frequency Shift Keying (FSK) as a robust method for digital data transmission. Specifically, the experiment aims to:
*	Implement the generation of an FSK signal using a Voltage Controlled Oscillator (VCO) method, where a digital message from a Sequence Generator controls the switching between two distinct frequencies.
*	Differentiate between the "space frequency" (logic 0) and the "mark frequency" (logic 1) to understand how frequency variations represent binary data.
*	Demonstrate a demodulation technique by using a selective filter to isolate one of the FSK sinewaves and an envelope detector to extract the digital information.
*	Analyze the noise immunity advantages of frequency modulation and utilize a comparator to restore the recovered signal from distortion, ensuring the digital integrity of the final output.

---

# III. MATERIALS

| Item | Description |
| :--- | :--- |
| **Trainer Unit** | Emona Telecoms-Trainer 101 (plus power-pack) |
| **Oscilloscope** | Dual channel 20MHz oscilloscope |
| **Leads (Scope)** | Three Emona Telecoms-Trainer 101 oscilloscope leads |
| **Leads (Patch)** | Assorted Emona Telecoms-Trainer 101 patch leads |

---

# IV. EXPERIMENTAL RESULTS

# 1. PART A – Generating an FSK Signal
To initiate the generation of a Frequency Shift Keying (FSK) signal, the oscilloscope is configured for a stable, high-fidelity display by setting the Trigger Source to EXT with HF REJ coupling and both input channels to DC coupling. The Sequence Generator is prepared by setting its dip-switches to 00 to model the digital message, using its SYNC output to provide a steady trigger for the scope's 0.5ms/div timebase. The Voltage Controlled Oscillator (VCO) module serves as the FSK generator, with its Range set to LO, Gain at the midpoint, and the Frequency Adjust positioned at approximately a quarter of its travel (the 9 o’clock position). By switching the scope to DUAL mode, the original digital signal and the resulting FSK waveform can be compared simultaneously, with minor adjustments to the VCO's frequency control used to stabilize any rolling of the sinewaves.

## 1.1 Experiment Circuit Procedure
The Sequence Generator module is employed to model the digital data signal, with its SYNC output connected to the oscilloscope's trigger to ensure a stable and synchronized display. To generate the FSK signal, the VCO module is used, shifting its output frequency in response to the logic levels of the digital message.

<img width="585" height="310" alt="P1" src="https://github.com/user-attachments/assets/5d20a613-0ccb-4a4b-8c7b-68664262d690" />

<img width="565" height="325" alt="P2" src="https://github.com/user-attachments/assets/309c6b24-331c-48ba-9268-5784203d76ce" />

## OBSERVATION

![F1](https://github.com/user-attachments/assets/f49214b4-d8d6-4629-b1a1-288b7ee422b3)

The final oscilloscope capture in the series demonstrates the successful generation of a Frequency Shift Keying (FSK) signal using the VCO switching method. The red trace (Channel 1) shows the digital data pulse, while the yellow trace (Channel 2) displays the frequency-modulated carrier wave. Unlike the previous ASK experiment where the carrier was turned on and off, the FSK waveform remains continuous but shifts its frequency in direct response to the digital input. When the data is at a logic low, the carrier oscillates at a lower "space frequency," visible as a more spread-out sinewave. As the digital signal transitions to a logic high, the VCO module immediately increases the output to a higher "mark frequency," resulting in the more tightly packed sinusoidal cycles seen during the pulse interval. This visual confirmation proves that the digital information is successfully encoded into the frequency of the carrier, providing the basis for a transmission system that is naturally resistant to amplitude-based noise.

# 2. PART B – Demodulating an FSK signal using filtering and an envelope detector
Since FSK is a form of frequency modulation, it can be recovered using any standard FM demodulation scheme; however, because it only switches between two specific frequencies, a unique filtering method can be employed. In this procedure, the VCO module's Frequency Adjust is set to the 2 o'clock position while the Tuneable Low-pass Filter (LPF) is initially set with its Gain and Cut-off Frequency controls fully clockwise. The Tuneable LPF is used to isolate one of the two FSK sine waves by slowly turning the cut-off frequency control counter-clockwise until the higher frequency component is attenuated to zero. Once isolated, the signal is passed through a rectifier and a baseband LPF, which together function as an envelope detector to complete the demodulation process. The resulting output is then compared to the original digital signal on the oscilloscope to verify successful recovery.

## 2.1 Experiment Circuit Procedure

<img width="658" height="294" alt="P3" src="https://github.com/user-attachments/assets/332df57a-6b4b-428c-ab34-b90359d6e77a" />

<img width="705" height="269" alt="P4" src="https://github.com/user-attachments/assets/e1b484e4-9244-4a1f-ab25-c78566f24688" />

## OBSERVATION

![F2](https://github.com/user-attachments/assets/545aebb3-47d6-4009-8702-146048e90ff0)

The observation of the FSK demodulation process reveals how frequency-selective filtering transforms the signal for data recovery. As instructed, the Tuneable Low-pass Filter is adjusted to isolate the lower "space" frequency by effectively attenuating the higher "mark" frequency component to zero. On the oscilloscope, the yellow trace represents the output of the filter, while the red trace shows the original digital signal. When the digital message is at a logic low, the filter allows the lower frequency sinewave to pass through; however, when the message transitions to a logic high, the resulting waveform drops to zero because the filter’s cut-off frequency has been set to block that higher frequency. This conversion effectively turns the FSK signal into an ASK-like signal, where the presence or absence of a carrier now corresponds to the digital logic levels. By then passing this filtered output through the rectifier and baseband LPF, the "envelope" can be traced to successfully recover the original digital bitstream.

## 2.2 Experiment Circuit Procedure

<img width="569" height="263" alt="P5" src="https://github.com/user-attachments/assets/352bf482-2f10-48d9-942c-265cbacb3ec0" />

## OBSERVATION

![F3](https://github.com/user-attachments/assets/500654c4-195a-4ffa-a8f3-0636d4bfccce)

The final observation shows the restored digital signal after passing through the comparator. While the output from the envelope detector is rounded and distorted due to the filtering process, the comparator uses a DC reference threshold to regenerate the sharp, rectangular edges of the original sequence. The final yellow trace on the scope is a clean, squared-up digital signal that perfectly matches the timing and logic levels of the original red message, confirming the successful recovery of the FSK-encoded data.

# 3. PART C- Restoring the recovered data using a comparator
Building on the principles from Experiment 14, a comparator is utilized in this final stage to effectively "clean up" and restore the integrity of the demodulated FSK signal. Because the amplitude of the filtered signal entering the comparator fluctuates between zero volts and a peak level, the Variable DCV module is set to provide a threshold voltage equal to half of that maximum level. By comparing the original digital message to the output of the comparator and making slight adjustments to the DC voltage control, the distorted, rounded waveform is transformed back into a sharp, rectangular signal that matches the original data stream.

## 3.1 Experiment Circuit Procedure

<img width="695" height="300" alt="P6" src="https://github.com/user-attachments/assets/6b4fa3fd-14e3-436d-bcf1-8f3b40db94b9" />

<img width="689" height="275" alt="P7" src="https://github.com/user-attachments/assets/b4cd9b93-e3b1-47e1-9098-ec0ca1910b6b" />

# OBSERVATION

![F4](https://github.com/user-attachments/assets/e0cc1af9-523f-4384-a4d1-0021673a6c46)

The oscilloscope display shows the original digital sequence on the red trace (Channel 1) and the comparator’s restored output on the yellow trace (Channel 2).
By comparing the two, it is evident that the comparator has successfully transformed the distorted, rounded signal from the envelope detector back into a clean, rectangular bitstream. The yellow pulses now have sharp, vertical rising and falling edges that align precisely with the timing of the original message. This confirms that the Variable DCV module was correctly set to a threshold level that allowed the comparator to accurately "square up" the signal, effectively eliminating the rounding introduced during the filtering and demodulation stages. The final result is a high-integrity digital signal that is ready for further processing or decoding.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What's the name for the VCO output frequency that corresponds with logic-1s in the digital data?**

Answer: The frequency corresponding with logic-1s is known as the mark frequency.

**Question 2: What's the name for the VCO output frequency that corresponds with the logic-0 in the digital data?**

Answer: The frequency corresponding with logic-0s is known as the space frequency.

**Question 3: Based on your observations of the FSK signal, which of the two is the higher frequency? Explain your answer.**

Answer: The mark frequency is the higher frequency. This is observed in the oscilloscope traces (such as image_e17c8d.jpg), where the sinusoidal cycles are more "tightly packed" together when the digital signal is high, indicating a shorter period and thus a higher frequency compared to the more spread-out "space" oscillations.

**Question 4: Which of the FSK signal's two sinewaves is the filter picking out?**

Answer: The filter is configured to pick out the lower frequency (the space frequency). This is achieved by lowering the cut-off frequency until the higher frequency component is attenuated to zero.

**Question 5: What does the filtered FSK signal look like?**

Answer: The filtered signal resembles an ASK (Amplitude Shift Keying) signal. As seen in your oscilloscope traces, the sinewave is present when the digital data is at logic-0 but becomes a flat line (zero volts) when the data is at logic-1 because the higher frequency has been blocked.

**Question 6: What can be used to "clean-up" the recovered digital signal?**

Answer: A comparator is used to clean up the signal.

**Question 7: How does the comparator turn the slow rising voltages of the recovered digital signal into sharp transitions?**

Answer: The comparator acts as a high-gain switching circuit that compares the incoming rounded voltage against a fixed DC reference threshold. As soon as the rising edge of the distorted signal crosses this threshold, the comparator's output instantly switches to its maximum logic level, effectively regenerating the vertical edges and "squaring up" the waveform.

---

# VI. Conclusion
Based on the results of the Frequency Shift Keying experiment, the following conclusions summarize the generation, demodulation, and restoration process:
*	FSK Generation and Frequency Logic: We proved that a Voltage Controlled Oscillator (VCO) can effectively encode digital data by switching between a lower "space frequency" for logic 0 and a higher "mark frequency" for logic 1. This continuous-wave approach provides superior noise immunity compared to ASK, as information is stored in frequency shifts rather than amplitude.
*	Demodulation via Frequency Isolation: Our investigation confirmed that FSK can be demodulated using a unique filtering method; by setting a Tuneable Low-pass Filter to attenuate the higher mark frequency, we effectively converted the FSK signal into an ASK-like waveform. This proved that isolating a single frequency component is a viable first step in recovering binary data.
*	The Filtering Trade-off: We observed that while the envelope detector (rectifier and baseband LPF) successfully stripped the remaining carrier to reveal the digital envelope, the process introduced significant rounding. This rounding occurred because the filter removed the high-frequency harmonics necessary for sharp transitions, resulting in a distorted version of the original bitstream.
*	Data Restoration and Thresholding: We demonstrated the critical role of the Voltage Comparator in restoring signal integrity. By comparing the rounded envelope against a mid-point DC reference threshold, we leveraged high-gain switching to regenerate the sharp, rectangular edges of the original 00-bit sequence.
*	System Robustness: Finally, the experiment solidified that despite the distortion introduced during the analog stages of filtering and demodulation, threshold-based logic allows for the near-perfect reconstruction of the digital signal. This reinforces the reliability of FSK as a robust method for maintaining data integrity across an analog communication channel.
