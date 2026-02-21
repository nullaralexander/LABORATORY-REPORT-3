# EXPERIMENT 18: Quadrature Phase Shift Keying 
---

# I. INTRODUCTION
Building on the principles of phase modulation, Quadrature Phase Shift Keying (QPSK) is a sophisticated variation of BPSK that doubles the efficiency of the radio-frequency spectrum by transmitting two bits of digital information simultaneously. Unlike BPSK, which processes bits individually, a QPSK modulator utilizes a "bit-splitter" to divide the data stream into even and odd bits. The even bits are multiplied with a carrier to create one BPSK signal (PSKi), while the odd bits are multiplied with the same carrier—phase-shifted by 90°—to create a second BPSK signal (PSQq). Although the combined signal occupies the same bandwidth as a single BPSK transmission, the receiver can separate the two data streams using phase discrimination, leveraging the fact that a product detector completely rejects a signal if its local carrier is exactly 90° out of phase with the transmitted carrier. Consequently, while QPSK does not increase the overall transmission speed due to the halving of the bit-rate during the split, it effectively allows more users to share the channel by requiring only half the spectrum of BPSK. In this experiment, the Emona Telecoms-Trainer 101 will be used to implement the mathematical model of QPSK, examine the resulting waveform, and demonstrate how a product detector can isolate specific data sets through phase-sensitive recovery.

---

# II. OBJECTIVE
OBJECTIVE
The objectives of Experiment 18 are designed to explore the spectral efficiency and phase-sensitive nature of Quadrature Phase Shift Keying (QPSK). Specifically, the experiment aims to:
*	Implement the mathematical model of a QPSK generator using the Emona Telecoms-Trainer 101 to understand how even and odd bits are modulated onto orthogonal carriers.
*	Analyze the QPSK waveform to observe how two independent BPSK signals can occupy the same portion of the radio-frequency spectrum simultaneously.
*	Demonstrate the principle of bit-splitting, where a single data stream is divided into bi-pairs to halve the required transmission bandwidth.
*	Investigate phase discrimination by using a product detector to selectively pick out one of the two modulated data streams while rejecting the other.
*	Verify the 90° phase error relationship, confirming that a product detector completely rejects a message if the local carrier and transmission carrier are in quadrature.

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

# 1. PART A – Generating a QPSK signal
To initiate the generation of a Quadrature Phase Shift Keying (QPSK) signal, the oscilloscope is configured for a stable display by setting the Trigger Source to EXT with HF REJ coupling and both input channels to DC coupling. Using a 0.5ms/div timebase, the Sequence Generator is employed to model the digital data, while the 2-bit Serial-to-Parallel Converter module acts as the bit-splitter to divide the data into separate streams of even and odd bits. Because this splitting process inherently halves the bit rate of the data streams, a Divider module must be set to divide by 2 (with the left switch up and right switch down) to process the Sequence Generator's SYNC output. This ensures that the triggering signal for the oscilloscope is appropriately halved, maintaining a synchronized and accurate visual representation of the lower-rate QPSK components.

## 1.1 Experiment Circuit Procedure
In this setup, the Sequence Generator module is utilized to model the digital data, while the 2-bit Serial-to-Parallel Converter module functions as a bit-splitter to divide the data into distinct streams of even and odd bits. As noted in the preliminary discussion, this splitting process effectively halves the bit rate for both resulting data sets. Consequently, the SYNC output from the Sequence Generator must be passed through a divider to be halved before it can serve as a stable triggering signal for the oscilloscope.

<img width="467" height="243" alt="P1" src="https://github.com/user-attachments/assets/6f536110-12de-435f-be12-5139596dfc28" />

<img width="464" height="303" alt="P2" src="https://github.com/user-attachments/assets/de716f7e-cf6d-4356-9910-44aa126c0f64" />

## OBSERVATION

![P1](https://github.com/user-attachments/assets/839c67eb-0d72-4ab5-ab55-dae7cfd30339)

The observation of the Quadrature Phase Shift Keying (QPSK) generation process highlights the critical role of bit-splitting and timing synchronization. The oscilloscope display demonstrates the relationship between the two independent bit streams created by the 2-bit Serial-to-Parallel Converter. The red trace on Channel 1 and the yellow trace on Channel 2 represent the even and odd bit streams respectively, both operating at exactly half the bit rate of the original master data stream. By utilizing the Divider module to halve the SYNC output from the Sequence Generator, a stable trigger is achieved, allowing for a clear comparison of these parallel digital signals. This visual confirmation proves that the single high-speed serial input has been successfully converted into two slower parallel streams, which serves as the foundation for modulating them onto quadrature carriers in the subsequent stages of the experiment.

## 1.2 Experiment Circuit Procedure
The experimental setup for generating the QPSK signal utilizes two independent Multiplier modules, each receiving one of the bit-splitter's outputs. To satisfy the specific requirements of Quadrature Phase Shift Keying, a 100kHz sine wave is fed into these multipliers, with the two carrier signals maintained at a 90° phase shift relative to each other. By setting the oscilloscope timebase to 0.2ms/div and activating the Sweep Multiplier, the even bits of the data can be closely compared to the resulting PSKi output. Utilizing the horizontal position control to pinpoint a transition in the data sequence allows for a detailed examination of the carrier, revealing how the waveform's phase characteristics change in response to logic level shifts.

<img width="574" height="273" alt="P3" src="https://github.com/user-attachments/assets/0022e8f3-a8e9-4c14-b79a-6f471515d8db" />

<img width="431" height="330" alt="P4" src="https://github.com/user-attachments/assets/7c59819c-66fe-40eb-84f8-f4779640f6c8" />

## OBSERVATION

![P2 1](https://github.com/user-attachments/assets/0292adb1-53af-47f3-993c-cf1ee8a50106) ![P2 2](https://github.com/user-attachments/assets/ab060777-76bc-4f2b-8b38-d88eae258150)

When the Sweep Multiplier is deactivated (or the Timebase is at a standard 0.5ms/div), the oscilloscope provides a "macro" view of the signal. This allows you to see a longer sequence of the digital data and the general behavior of the carrier over several bits. Conversely, when the Sweep Multiplier is activated (the images on the left), the scope "zooms in" on a specific section of the waveform. This is what allowed you to see the individual cycles of the 100kHz carrier and the exact 180° phase reversal that occurs at the logic transitions.

## 1.3 Experiment Circuit Procedure
To complete the QPSK modulator setup, first deactivate the oscilloscope's Sweep Multiplier and return the Timebase control to the 0.5ms/div setting. The Adder module is then used to combine the PSKi and PSKq signals to form the full QPSK output. Begin by turning the Adder module's G control fully counter-clockwise to remove the PSKi signal from the output, then adjust the g control to achieve a 4Vp-p signal. Next, disconnect the patch lead from the Adder's B input to isolate the PSKq signal and adjust the G control until a 4Vp-p output is obtained. Finally, reconnect the patch lead to the B input to sum both signals, completing the quadrature modulation process.

<img width="539" height="230" alt="P5" src="https://github.com/user-attachments/assets/e3e1318f-e72c-4d40-8b26-f1b95f1c4667" />

<img width="582" height="324" alt="P6" src="https://github.com/user-attachments/assets/87a902de-95a6-4114-a5b4-a56486d49f43" />

## OBSERVATION

![P4](https://github.com/user-attachments/assets/3ddaee1a-9fb8-4189-9769-bc8075546590)

The observation of the final QPSK signal generation reveals the complex interaction between the two independent BPSK branches once they are combined by the Adder module. As shown in the oscilloscope captures with a timebase of 0.5ms/div, the process began by balancing the individual amplitudes of the and branches to exactly 4Vp-p to ensure a symmetrical constellation. When both signals are summed via the Adder's inputs, the resulting yellow trace represents the complete QPSK waveform, which exhibits a more intricate envelope compared to a single BPSK signal. Because the two carriers are 90° out of phase, their summation creates a composite signal where the phase shifts are no longer limited to simple 180° reversals; instead, the transitions between the four possible logic states (00, 01, 11, 10) result in phase changes of ±90° or 180°. This visual confirmation proves that the modulator has successfully merged two parallel data streams into a single band-limited signal, effectively doubling the spectral efficiency of the transmission.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What is the relationship between the bit rate of these two digital signals and the bit rate of the Sequence Generator module's output?**

Answer: The bit rate of the two digital signals (the even and odd bit streams) is exactly half the bit rate of the original Sequence Generator module's output. This occurs because the bit-splitter divides the serial data into two parallel streams, meaning each new stream only carries every second bit of the original data.

**Question 2: What feature of the Multiplier's output suggests that it's a BPSK signal?**

Answer: The presence of 180° phase reversals in the carrier wave at the exact moments of the digital data's logic transitions suggests that the output is a BPSK signal.

**Question 3: What type of signal is present on the Multiplier's output?**

Answer: The signal present on the Multiplier's output is a Double-Sideband Suppressed Carrier (DSBSC) signal.

**Question 4: According to the theory, what type of digital signal transmission is now present on the Adder's output?**

Answer: The Adder's output contains a Quadrature Phase Shift Keying (QPSK) signal. This is a complete digital transmission that carries two bits of information simultaneously within the same frequency spectrum.

**Question 5: Why is there only one sinewave when the QPSK signal is made up of two BPSK signals**

Answer: There is only one sine wave because both BPSK signals share the same carrier frequency. When two sine waves of the identical frequency are added together—even if they have different phases—the result is always a single combined sine wave at that same frequency, with its own specific resulting phase and amplitude.

---

# VI. Conclusion
In conclusion, Experiment 18 successfully demonstrated the generation and fundamental characteristics of Quadrature Phase Shift Keying (QPSK) through a multi-stage modulation process. The following points summarize the experimental findings:
*	Spectral Efficiency through Bit-Splitting: The experiment confirmed that QPSK improves spectral efficiency by utilizing a 2-bit Serial-to-Parallel Converter to split a high-speed data stream into two lower-rate parallel streams (even and odd bits). This process effectively halves the bit rate of each individual stream, as verified by the necessary use of a Divider module to synchronize the oscilloscope trigger.
*	BPSK as a Building Block: By examining the branch individually using the Sweep Multiplier, we observed distinct 180° phase reversals at logic transitions. This validated that each half of a QPSK signal functions as an independent BPSK (DSBSC) signal.
*	Quadrature Summation: The use of the Adder module to combine the and signals—each modulated-on carriers with a 90° phase shift—resulted in a single composite waveform. Balancing both branches to 4Vp-p ensured a symmetrical signal capable of representing four distinct logic states (00, 01, 11, and 10).
*	Phase Complexity: Unlike basic BPSK, the final QPSK output exhibited a more intricate envelope with phase shifts of ±90° or 180°. This confirms the theoretical secret of QPSK: by maintaining a 90° separation between carriers, two sets of data can occupy the same portion of the radio-frequency spectrum, doubling the amount of information transmitted without increasing bandwidth.
