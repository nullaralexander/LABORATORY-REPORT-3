# EXPERIMENT 19: DSSS Modulation and Demodulation 
---

# I. INTRODUCTION
Direct Sequence Spread Spectrum (DSSS) is an advanced variation of the DSBSC modulation scheme that utilizes a pulse train, known as a pseudo-noise (PN) sequence, as a carrier instead of a standard sinewave. Because pulse trains are composed of a fundamental frequency and an infinite number of harmonics, DSSS effectively acts as the DSBSC modulation of a theoretically infinite number of sinusoidal carriers, resulting in message information being distributed across a vast number of tiny sideband pairs. This unique distribution makes DSSS signals exceptionally robust against deliberate interference or "jamming" and provides a level of inherent encryption, as the receiver must use an identical, synchronized PN sequence to successfully reconstruct the original message from the noise-like transmission. Furthermore, increasing the sequence's chip-length distributes the signal's energy so thinly that it can become indistinguishable from background electrical noise, making the transmission difficult to detect. Widely used in technologies such as GPS, CDMA, and Wi-Fi, DSSS will be explored in this experiment using the Emona Telecoms-Trainer 101 to model the modulation process, demonstrate the necessity of correct sequence matching for demodulation, and investigate the system's inherent resistance to jamming.

---

# II. OBJECTIVE
The objectives of Experiment 19 are designed to explore the mechanics and advantages of Direct Sequence Spread Spectrum (DSSS) modulation. Specifically, the experiment aims to:
*	Implement the mathematical model of a DSSS generator using the Emona Telecoms-Trainer 101 by multiplying a message signal with a pseudo-noise (PN) sequence.
*	Demonstrate the process of DSSS demodulation using a product detector and a "stolen" carrier to successfully recover the original message.
*	Evaluate the critical importance of sequence synchronization, verifying that the receiver's local PN sequence must match the transmitter's sequence in both code and phase to avoid "garbage" noise-like outputs.
*	Investigate the inherent security and encryption properties of DSSS, noting how longer chip-length sequences increase the difficulty of unauthorized signal detection and decoding.
*	Observe the system's robustness by examining the difficulty of jamming a spread spectrum signal compared to traditional narrowband modulation schemes.

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

# 1. PART A – Generating a DSSS signal using a simple message
To generate a Direct Sequence Spread Spectrum (DSSS) signal, the system implements the mathematical model of DSBSC by substituting a standard sinusoidal carrier with a pulse train. After setting up the oscilloscope and ensuring the Trigger Source is set to CH1 with HF REJ coupling, the Sequence Generator dip-switches are set to 00 (both switches up) to define the specific PN sequence. The scope's Timebase is then adjusted to display approximately two cycles of the 2kHz SINE output from the Master Signals module, which serves as the message signal. Finally, by switching the scope to DUAL mode and adjusting the Vertical Attenuation, both the original message and the resulting DSSS output from the Multiplier module can be monitored simultaneously for comparison.

## 1.1 Experiment Circuit Procedure
The modulation process involves the multiplication of the 2kHz sine wave message signal with a 32-bit pulse train output from the Sequence Generator, which serves as the pseudo-noise (PN) sequence model.

<img width="783" height="437" alt="image" src="https://github.com/user-attachments/assets/5c4249b8-0cce-474f-a504-2d0477c0583a" />

<img width="783" height="502" alt="image" src="https://github.com/user-attachments/assets/de8bcb35-fd76-4823-b58c-7bd44a5c0a35" />

## OBSERVATION

<img width="478" height="358" alt="image" src="https://github.com/user-attachments/assets/d5995d4e-904e-43b6-83c6-2da607267b10" />

The observation of the DSSS generation process reveals the transformation of a low-frequency analog message into a wideband, noise-like signal through multiplication with a pseudo-noise sequence. As seen in the provided oscilloscope display, the 2kHz sine wave (red trace) acts as the message signal, while the resulting DSSS output (yellow trace) from the Multiplier module appears as a series of high-frequency bursts and phase reversals. Because DSSS is a variation of DSBSC using a pulse train as a carrier, the output waveform shows the sine wave message being "chopped" by the 32-bit PN sequence chips. Every time the PN sequence undergoes a logic transition, the phase of the carrier—represented here by the high-frequency components within the envelope—reverses, effectively spreading the signal's energy across a much wider frequency spectrum. This visual confirmation proves that the original message is no longer a simple narrowband signal but has been successfully encoded into a complex, spread-spectrum transmission that is inherently resistant to interference.

# 2. PART B – Generating a DSSS signal using speech

## 2.1 Experiment Circuit Procedure
In the next stage of the experiment, the modulation of a Direct Sequence Spread Spectrum (DSSS) signal is observed using a complex speech input rather than a simple sine wave. To begin this process, the patch lead is disconnected from the Master Signals module's 2kHz SINE output to clear the previous message. The oscilloscope's Timebase control is then adjusted to the 2ms/div setting, providing a wider viewing window suitable for the dynamic frequencies found in human voice. By talking, singing, or humming into the system's input, the display reveals how the pseudo-noise (PN) sequence from the Sequence Generator continues to rapidly switch the phase of the carrier, spreading the unpredictable and varying amplitudes of the speech message across the wide frequency spectrum.

<img width="783" height="430" alt="image" src="https://github.com/user-attachments/assets/b62d3a76-74a4-47fe-90c7-e5c8af42a67e" />

## OBSERVATION
 
<img width="478" height="566" alt="image" src="https://github.com/user-attachments/assets/bed46aa5-2c5d-44cb-86c6-5e1a20f8b87a" />

The observation of the DSSS generation using speech confirms that the modulation process effectively handles complex, real-time analog signals in the same manner as basic periodic waveforms. As shown in the oscilloscope capture with a 2ms/div timebase, the red trace represents the dynamic and unpredictable nature of the speech input, which lacks the uniformity of the previous sine wave message. Despite this complexity, the yellow trace reveals that the Multiplier module successfully spreads the speech signal by continuously switching its phase according to the high-speed PN sequence. The resulting output waveform demonstrates that while the envelope varies in response to the vocal amplitudes, the underlying carrier remains suppressed and spread across a wide frequency spectrum, rendering the information noise-like and difficult to intercept without the correct synchronized code. This visual data proves the system's ability to maintain the integrity of a voice transmission while providing the inherent security and interference resistance characteristic of spread spectrum technology.

# 3. PART C- Using the product detector to recover the message
To implement the recovery of the original message from the DSSS signal, the oscilloscope's Timebase is first returned to the 0.1ms/div position to provide a clear view of the demodulation process. The Multiplier and Tuneable Low-pass Filter modules are then utilized to form a product detector, which requires a local carrier that is identical to the one used at the transmitter. For this setup, the PN sequence is "stolen" from the Sequence Generator’s X output to serve as the local carrier, ensuring frequency and phase synchronization. With the filter’s Gain set to its midpoint and the Cut-off Frequency initially turned fully counter-clockwise, the control is slowly rotated clockwise to approximately half its travel. This filtering action removes the high-frequency components produced by the multiplication process, effectively reconstructing the original message for final observation and recording on the graph paper.

## 3.1 Experiment Circuit Procedure
The demodulation stage utilizes the Multiplier and Tuneable Low-pass Filter modules to function as a product detector, which is responsible for extracting the original message from the complex DSSS signal. To ensure the detector works effectively, a local carrier is provided by "stealing" the identical PN sequence from the transmitter’s X output, satisfying the requirement for perfect synchronization.

<img width="783" height="788" alt="image" src="https://github.com/user-attachments/assets/b1bbbb87-26cc-4e98-ab5d-74c516f6f628" />

<img width="783" height="445" alt="image" src="https://github.com/user-attachments/assets/0dac79fb-5929-4bc2-ab05-f75e05f499b6" />

# OBSERVATION
<img width="478" height="333" alt="image" src="https://github.com/user-attachments/assets/b5bf1430-7309-4a9e-ada3-823c46772496" />

The observation of the DSSS demodulation process demonstrates the effective reconstruction of the original message through synchronized product detection and low-pass filtering. As shown in the oscilloscope display, the top trace (red) represents the master 2kHz sine wave message, while the bottom trace (yellow) captures the output of the Tuneable Low-pass Filter. By "stealing" the identical PN sequence from the transmitter's X output to serve as the local carrier, the Multiplier module successfully reverses the spreading process, realigning the message energy into its original frequency band. The subsequent adjustment of the filter's Cut-off Frequency to approximately half its travel provides the necessary smoothing to remove high-frequency products and residual PN chips. This results in a recovered sinusoidal waveform that mirrors the frequency and phase of the original input, visually confirming that a wideband DSSS signal can be accurately collapsed back into a narrowband message provided the receiver possesses the exact, synchronized pseudo-noise code.

# 4. PART D- DSSS and deliberate interference (jamming)
In this section of the experiment, the resilience of Direct Sequence Spread Spectrum (DSSS) against deliberate interference, or jamming, is evaluated by introducing an unwanted signal into the transmission channel. After ensuring the product detector is correctly recovering the message by reconnecting the Sequence Generator's X output, the VCO module is configured as a variable-frequency jamming source by setting its Range to HI and its Frequency Adjust to the midpoint. The Adder module is then used to combine this jamming signal with the DSSS signal; by slowly turning the Adder's g control clockwise to its midpoint, the interference is introduced while the oscilloscope monitors the impact on the recovered message on Channel 2. Even as the jamming signal's frequency is varied across its range and its amplitude is increased to the maximum setting, the DSSS system's ability to maintain a clear recovered message is observed. This demonstrates the significant advantage of spread spectrum technology: because the message energy is distributed across a wide bandwidth, a narrowband jamming signal only affects a tiny fraction of the total signal power, allowing the receiver to effectively ignore the interference during the de-spreading process.

## 4.1 Experiment Circuit Procedure
To model deliberate interference, the VCO module serves as a source for a variable-frequency jamming signal, which is subsequently combined with the DSSS signal via the Adder module. This setup allows for a practical demonstration of how spread spectrum technology maintains signal integrity even when an external interferer is introduced into the transmission channel.

<img width="783" height="418" alt="image" src="https://github.com/user-attachments/assets/47b7b4aa-a08c-44d6-bc25-ee49f5176308" />

<img width="783" height="332" alt="image" src="https://github.com/user-attachments/assets/f3e4b16b-8e81-4f91-83b6-2465cebf80cd" />

# OBSERVATION

<img width="478" height="369" alt="image" src="https://github.com/user-attachments/assets/0f09f283-0f1c-47ca-8b8f-ac62673509e6" />

The observation of DSSS under deliberate interference highlights the system's remarkable robustness and its inherent resistance to narrowband jamming. As illustrated in the final oscilloscope capture, the red trace (Channel 1) represents the DSSS signal combined with a high-amplitude jamming signal from the VCO module. While the transmitted signal appears heavily distorted and dominated by the interferer, the yellow trace (Channel 2) shows the recovered message remaining clearly identifiable and relatively stable. This occurs because the product detector uses an identical PN sequence to "de-spread" the desired signal while simultaneously "spreading" the narrowband jamming signal into wideband noise. Even as the jamming signal’s frequency is varied and its amplitude is increased to the maximum setting via the Adder’s g control, the message integrity is preserved. This visual evidence confirms that because DSSS distributes message energy across a vast number of sidebands, a single-frequency jammer can only disrupt a negligible portion of the total signal, allowing the receiver to effectively filter out the interference.

## 4.2 Experiment Circuit Procedure
To further challenge the system's resilience, a more sophisticated broadband jamming approach is employed by utilizing a Noise Generator module to simulate thousands of simultaneous jamming frequencies. By adding this broadband noise to the DSSS signal via the Adder module, the oscilloscope reveals that while the transmitted DSSS waveform becomes significantly distorted, the recovered message remains only mildly affected. The intensity of this interference is then systematically increased by switching the Adder’s input to the Noise Generator’s -6dB and eventually the 0dB outputs. Remarkably, even at maximum interference levels where the DSSS signal is visually overwhelmed by noise, the product detector successfully extracts the original message with minimal degradation. This final demonstration confirms that the processing gain of spread spectrum technology allows it to effectively reject even high-power, broadband interference that would typically render traditional narrowband communications impossible.

<img width="783" height="787" alt="image" src="https://github.com/user-attachments/assets/0ee7693c-67bd-446a-8910-d6714b8fad91" />

# OBSERVATION

<img width="478" height="419" alt="image" src="https://github.com/user-attachments/assets/8f62ebbd-ac7d-48fc-9f62-1fa6e230d57c" />

The observation of DSSS under broadband jamming further validates the technology's exceptional immunity to high-power, multi-frequency interference. As seen in the provided oscilloscope captures, the red traces (Channel 1) represent the DSSS signal being progressively buried under noise as the Noise Generator output is increased from -6dB to 0dB. At the highest interference level, the transmitted signal is visually indistinguishable from random noise, representing a "jammed" environment that would typically destroy standard communication. However, the yellow traces (Channel 2) demonstrate that the product detector continues to extract a recognizable recovered message with only slight jitter and mild distortion. This outcome is a direct result of the system's processing gain; during demodulation, the receiver's local PN sequence collapses the wideband message back into its original narrow bandwidth while simultaneously spreading the broadband noise even further, effectively thinning its power density. These results provide conclusive evidence that DSSS remains functional in extreme interference conditions, maintaining signal integrity even when the channel is flooded with a broad spectrum of noise.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What feature of the Multiplier module's output suggests that it's basically a DSBSC signal?**

Answer: The most prominent feature suggesting a DSBSC (Double Sideband Suppressed Carrier) structure is the presence of phase reversals whenever the carrier (in this case, the PN sequence) or the message changes polarity. Additionally, the output waveform lacks a visible constant carrier component, showing that the carrier is suppressed and its energy is redistributed into the sidebands.

**Question 2: Why is the DSSS signal so large when it's supposed to be small and indistinguishable from noise?**

Answer: In this laboratory environment, the DSSS signal appears large because the sequence length (number of chips) is relatively short (32 bits), meaning the energy is not yet distributed "thinly" enough to fall below the noise floor. In practical applications like GPS, the PN sequences are significantly longer—consisting of millions of chips—which spreads the total energy so widely across the spectrum that the power density of any individual component becomes smaller than the background electrical noise.

**Question 3: Why isn't there any signal out of the DSSS modulator when you're not talking, etc**

Answer: Because DSSS is a variation of DSBSC, the output is the result of multiplying the message by the carrier. Mathematically, if there is no input message ($m(t) = 0$), the product of the multiplication is zero. Without a voice or sine wave signal to modulate the PN sequence, there is no message energy to "spread," resulting in no output from the Multiplier module.

**Question 4: What does the signal out of the low-pass filter look like?**

Answer: The signal out of the low-pass filter is a reconstructed version of the original message, such as a clean 2kHz sine wave or the original speech audio. While it may contain a small amount of high-frequency "ripple" or jitter caused by the PN sequence transitions, the filtering process successfully removes the high-frequency "spread" components, leaving only the original narrowband message.

**Question 5: Why does using the wrong PN sequence for the local carrier cause the product detector's output to look like this?**

Answer: Using an incorrect or unsynchronized PN sequence results in a "garbage" signal that looks like noise because the tiny demodulated components are at the wrong frequency and phase. For successful reconstruction, every "chip" in the receiver's local carrier must perfectly match the transmitter's carrier in both code and timing so that the signals add up in-phase to reproduce the original message; otherwise, they cancel each other out or remain spread across the spectrum.

**Question 6: Why doesn't the jamming signal interfere with the recovery of the message?**

Answer: The jamming signal is effectively ignored due to processing gain. During demodulation, the receiver multiplies the incoming signal by the PN sequence, which "despreads" the desired message back into a narrowband signal. Simultaneously, this same process "spreads" the narrowband jamming signal (from the VCO) into wideband noise, significantly reducing its power density within the message's bandwidth and allowing the low-pass filter to reject most of the interference.

---

# VI. Conclusion
Experiment 19 successfully demonstrated the fundamental principles, implementation, and operational advantages of Direct Sequence Spread Spectrum (DSSS) modulation and demodulation. By utilizing the Emona Telecoms-Trainer 101, the following key conclusions were established:
*	Modulation Versatility: The experiment proved that DSSS effectively functions as a variation of DSBSC, where a high-speed 32-bit PN sequence acts as the carrier to "chip" and spread the bandwidth of both simple periodic sine waves and complex, dynamic speech signals.
*	Secure Recovery through Synchronization: Successful demodulation was shown to be entirely dependent on synchronization and code matching. By using a "stolen" identical PN sequence in a product detector, the receiver was able to "collapse" the wideband signal back into its original narrowband form.
*	Inherent Security and Detectability: The observations confirmed that DSSS signals are noise-like in the time domain, making them difficult to intercept or even detect without the exact pseudo-noise code, providing a layer of inherent encryption.
*	Superior Interference Immunity: The most significant finding was the system's resilience to both narrowband and broadband jamming. Due to processing gain, the receiver effectively despreads the desired message while simultaneously spreading the interfering signals into low-power background noise. Even when the transmitted signal was visually buried under 0dB of broadband noise, the original message was recovered with minimal degradation.

In summary, the experiment validated why DSSS is a critical technology for modern communication systems like GPS and Wi-Fi, offering a robust solution for maintaining signal integrity and security in highly congested or contested electronic environments.



