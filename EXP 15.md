# EXPERIMENT 15: Amplitude Shift Keying
---

# I. INTRODUCTION
This experiment explores the fundamental necessity of channel sharing in electronic communications, a concept critical for managing modern telecommunications infrastructure like mobile networks and fiber optics. While methods such as Time Division Multiplexing (TDM) allow multiple users to share a channel by interleaving data in short time slots, the resulting increase in bit rates often leads to signal distortion within limited bandwidths. To address this, Frequency Division Multiplexing (FDM) provides an alternative by assigning users specific frequency bands, requiring digital data to be superimposed onto a carrier wave through modulation.
A primary focus of this study is Amplitude Shift Keying (ASK), a digital version of amplitude modulation where the carrier's amplitude is switched on and off to represent logic levels. While ASK allows for simple data recovery via an envelope detector—as the signal's envelope mirrors the original data stream—it remains susceptible to channel noise that can corrupt the signal's shape. Throughout this procedure, an ASK signal will be generated using a switching method, recovered using an envelope detector, and ultimately "cleaned up" using a comparator to restore the original digital integrity.

---

# II. OBJECTIVE
The objective of this experiment is to investigate the generation and recovery of an Amplitude Shift Keying (ASK) signal as a method of Frequency Division Multiplexing. Specifically, the experiment aims to:
*	Model the generation of an ASK signal using a switching method, where a digital data stream controls the transmission of a high-frequency carrier wave.
*	Analyze the characteristics of the ASK waveform, noting how the signal's envelope corresponds to the original 1s and 0s of the digital message.
*	Implement a recovery circuit using a simple envelope detector to extract the digital information from the modulated carrier.
*	Evaluate the limitations of envelope detection, particularly the signal distortion caused by channel effects, and demonstrate how a comparator can be used to restore the signal to its original digital integrity.

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

# 1. PART A – Generating an ASK signal
To begin the generation of an Amplitude Shift Keying (ASK) signal, the equipment must be configured to provide a stable and accurate display of high-frequency digital transitions. The oscilloscope is set to DUAL mode with both channels using DC input coupling and a 1ms/div timebase, while the Trigger Source is set to EXT with HF REJ coupling to ensure synchronization with the system's timing signals. In this setup, the Sequence Generator module provides the digital data stream, and its SYNC output is connected to the scope's external trigger input to maintain a steady visual of the 32-bit sequence. To physically create the ASK waveform, a Dual Analog Switch module is utilized as the modulator, which will be viewed on Channel 2 alongside the original digital signal on Channel 1.

## 1.1 Experiment Circuit Procedure
The Sequence Generator module serves as the digital data source for the system, while its SYNC output is connected to the oscilloscope's external trigger to ensure a steady and synchronized display of the data stream. To create the modulated waveform, the Dual Analog Switch module acts as the modulator, switching a high-frequency carrier on and off to generate the ASK signal.

<img width="466" height="225" alt="p1" src="https://github.com/user-attachments/assets/9f1c351c-458f-4665-a7f8-6e7df7aada22" />

<img width="412" height="216" alt="p2" src="https://github.com/user-attachments/assets/99306e3a-50a7-45b1-ac14-45a83479ae1c" />

## OBSERVATION

![f1](https://github.com/user-attachments/assets/60359a0f-2b59-454c-bf04-4d30a60a0da9)

The red trace on the oscilloscope represents our original analog message, while the dense yellow area represents the sampled output created by the high-speed switching process. Because sampling is mathematically the multiplication of the message and the sampling signal, we can see the yellow pulses "tracking" the shape of the red sinewave, effectively using the message as an envelope. This specific visual result confirms the "natural" sampling technique, where the voltage of the pulses continues to change along with the message signal for the duration that the sampling gate remains open.

## 1.2 Experiment Circuit Procedure
In the current configuration, the ASK signal's carrier and the Sequence Generator clock both operate at 2 kHz from the same Master Signals source. While this synchronization makes the waveform easy to observe on the oscilloscope, it is impractical for a real-world communication system because the carrier frequency and the data signal's fundamental frequency are too close together. Such proximity makes recovering the digital information at the receiver difficult or even impossible. Ideally, the carrier frequency should be significantly higher than the bit rate of the digital signal. To achieve a more conventional and appropriate ASK signal, the carrier will be increased to approximately 100 kHz by setting the VCO module to the HF range and adjusting its frequency control to the midpoint of its travel.

<img width="703" height="294" alt="p3" src="https://github.com/user-attachments/assets/a422eb97-4810-4926-b893-bf2e89dc2386" />

<img width="678" height="291" alt="p4" src="https://github.com/user-attachments/assets/7918fbd7-6d32-478a-8385-686fbcd0e61f" />

## OBSERVATION

![f2](https://github.com/user-attachments/assets/4c62ce0f-4aec-49d4-ac7c-c874f88da8af)

The transition to a more conventional Amplitude Shift Keying (ASK) signal is clearly demonstrated as the carrier frequency is significantly increased. While the original digital message from the Sequence Generator remains visible as the top trace, the modulated output on the second channel now consists of dense, high-frequency bursts that represent the logic high states. By utilizing the VCO module in the HF range to reach approximately 100 kHz, a necessary frequency separation is established between the carrier and the digital bit rate. This adjustment moves the setup away from the impractical 2 kHz synchronized model and creates a waveform where the "on" and "off" states are sharply defined. This separation ensures that the digital information is successfully superimposed onto the carrier in a manner that allows a receiver to effectively track the signal's envelope for data recovery.

# 2. PART B – Decoding the PCM data
Since Amplitude Shift Keying (ASK) is essentially a form of amplitude modulation that carries a digital message rather than analog audio, it can be recovered using standard AM demodulation techniques. In this part of the experiment, an envelope detector is implemented using the rectifier on the Utilities module in conjunction with the Tuneable Low-pass Filter. To prepare the circuit for data recovery, the filter's Gain and Cut-off Frequency Adjust controls must both be rotated fully clockwise to ensure the recovered signal has sufficient amplitude and includes the necessary frequency components. This setup allows the receiver to strip away the high-frequency carrier and trace the "envelope" of the signal to extract the original digital bitstream.

## 2.1 Experiment Circuit Procedure

<img width="677" height="288" alt="p5" src="https://github.com/user-attachments/assets/6dce4149-533e-446c-b074-9f0cd690d8fa" />

<img width="717" height="322" alt="p6" src="https://github.com/user-attachments/assets/94cdf07c-e512-4d52-ae01-adae4b9cd7df" />

## OBSERVATION

![f3](https://github.com/user-attachments/assets/1a383ed7-7d38-4fb5-b14f-7b89878cb262)

Based on the experimental procedure for demodulating the ASK signal, the oscilloscope confirms the initial stage of data recovery using an envelope detector. The red trace (Channel 1) represents the recovered output from the Tuneable Low-pass Filter, while the yellow trace (Channel 2) shows the original digital bitstream from the Sequence Generator. By passing the modulated ASK signal through the rectifier and the filter, the high-frequency carrier has been effectively stripped away, leaving behind a waveform that tracks the "envelope" of the original pulses. However, the recovered red signal exhibits significant rounding and lacks the sharp, rectangular edges of the original yellow sequence. This occurs because the envelope detector's filtering process, while successful in removing the carrier, also attenuates the high-frequency harmonics necessary to maintain a perfect square wave, resulting in a continuous, sinusoidal-like representation of the digital data.required for commercial digital communication systems.

# 3. PART C- Restoring the recovered digital signal using a comparator
Building on the techniques from previous experiments, the final stage of the process utilizes a comparator to restore the integrity of the recovered digital signal. Because the output from the envelope detector is often rounded and distorted, the comparator serves as an essential tool to "clean up" the waveform by regenerating its sharp, rectangular edges. To prepare for this restoration, the Variable DCV module's control is set to the middle of its travel, providing an initial reference threshold for the comparator to distinguish between the high and low logic states of the demodulated ASK signal.

## 3.1 Experiment Circuit Procedure

<img width="703" height="313" alt="p7" src="https://github.com/user-attachments/assets/ecc31546-da81-4c57-b2f5-d00bea29a3bc" />

<img width="720" height="260" alt="p8" src="https://github.com/user-attachments/assets/c8622f4d-2491-4c79-8441-8f93ae4cee89" />

# OBSERVATION

![f4](https://github.com/user-attachments/assets/a8d783fc-3a80-4326-8756-3419fc117b5a)

The final stage of signal recovery is captured in the oscilloscope display, showcasing the successful restoration of the digital bitstream using a comparator. The red trace on Channel 1 represents the original digital data, while the yellow trace on Channel 2 displays the "cleaned-up" output from the comparator. By comparing the rounded, demodulated signal against the reference threshold set by the Variable DCV module, the comparator effectively regenerates the sharp, vertical rising and falling edges of the original square wave. The resulting yellow waveform is once again a rectangular digital signal with clear logic high and low levels, demonstrating that the comparator has successfully eliminated the distortion introduced by the envelope detector's filtering process. This observation confirms that while the intermediary recovery steps round the signal, the use of a high-gain switching device can perfectly restore the digital integrity of the ASK message for final decoding.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What is the relationship between the digital signal and the presence of the carrier in the ASK Signal?**

Answer: In an ASK signal, the digital message acts as a control for the carrier wave; specifically, the high-frequency carrier is switched "on" (present) when the digital signal is a Logic-1 and is switched "off" (absent) when the digital signal is a Logic-0.

**Question 2: What is the ASK signal's voltage when the digital signal is logic-0?**

Answer: When the digital signal is at Logic-0, the ASK signal’s voltage is ideally 0V, as the carrier wave is completely suppressed in a standard On-Off Keying (OOK) configuration. Briefly setting the Channel 2 Input Coupling to the GND position allows you to confirm this by seeing the signal align perfectly with the zero-volt reference line on the oscilloscope grid.

**Question 3: What feature of the ASK signal suggests that it's an AM signal?**

Answer: The feature identifying ASK as a form of Amplitude Modulation (AM) is that the information is encoded entirely by varying the amplitude (peak-to-peak voltage) of the carrier wave while its frequency and phase remain constant. The "envelope" of the ASK signal follows the shape of the modulating digital square wave, which is the defining characteristic of AM.

**Question 4: Why is the recovered digital signal not a perfect copy of the original?**

Answer: The recovered digital signal is not a perfect copy because the low-pass filter used in the demodulation process cannot instantly transition between states, resulting in rounded edges or "sloped" transitions instead of sharp vertical ones. Additionally, circuit noise and phase delays introduced by the hardware further distort the signal's timing and shape.

**Question 5: What can be used to "clean up" the recovered digital signal?**

Answer: To "clean up" the recovered signal and restore it to a proper digital format, a voltage comparator or a Schmitt Trigger is used to re-shape the pulses into a clean square wave.

**Question 6: How does the comparator turn the slow-rising voltages of the recovered digital signal into sharp transitions?**

Answer: A comparator creates sharp transitions by constantly comparing the slow-rising input voltage against a fixed reference voltage (Vref); because the comparator has extremely high gain, the moment the input voltage crosses the threshold, the output "snaps" almost instantly to its maximum or minimum voltage level.

---

# VI. Conclusion
 Our exploration of the ASK Generation and Recovery experiment has successfully demonstrated the principles of digital modulation and the critical steps required for accurate data transmission. By utilizing the Emona Telecoms-Trainer 101, we validated how digital data can be superimposed onto a high-frequency carrier and subsequently reconstructed through demodulation and restoration.
*	Modulation and Carrier Separation: We proved that while a digital signal can be used to switch a carrier "on" and "off," the frequency separation between the carrier and the bit rate is vital. Transitioning from an impractical 2 kHz carrier to a 100 kHz HF carrier established the necessary bandwidth for a stable, recognizable ASK signal.
*	The Demodulation Dilemma: We confirmed that an envelope detector (rectifier and low-pass filter) is effective at stripping away the high-frequency carrier. However, we observed that the filtering process introduces sloped transitions and rounding, as the filter removes the high-frequency harmonics required to maintain a perfect square wave.
*	Signal Restoration via Comparator: Our investigation into the restoration stage highlighted the essential role of the Voltage Comparator. By comparing the distorted, rounded signal against a DC reference threshold, we leveraged high-gain switching to regenerate sharp, vertical edges, effectively "cleaning up" the signal back to its original 32-bit digital state.
*	System Integrity: Finally, we noted that while the intermediary analog stages of a communication link (like filtering and transmission) naturally degrade the waveform, the use of threshold-based logic allows for the perfect reconstruction of the digital sequence, reinforcing the inherent robustness of digital communication systems.

This experiment solidifies our understanding of the ASK lifecycle: by respecting the mathematical and hardware requirements for carrier separation and threshold detection, we can ensure that digital information survives the transitions between the digital and analog domains.

