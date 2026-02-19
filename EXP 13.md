# EXPERIMENT 13: PCM Decoding

---

# I. INTRODUCTION
This experiment focuses on PCM decoding, the process of recovering an original message from a serial binary bitstream. To achieve this, the decoder must identify data frames, extract 8-bit binary numbers, and generate proportional voltages—ranging from -2V (00000000) to +2V (11111111). This creates a Pulse Amplitude Modulation (PAM) signal, which is then smoothed into an analog waveform using a low-pass filter.
Successful decoding relies on strict synchronization. Because the Emona Telecoms-Trainer 101 is not self-clocking, we will use a "stolen-signal" approach, providing the decoder with the exact clock (CK) and frame synchronization (FS) signals used by the encoder. Using this setup, we will convert sine waves and speech into PCM data and back again, demonstrating the precision required to accurately reconstruct digital data into its original analog form.

---

# II. OBJECTIVE
The primary goals of Experiment 13 are as follows:
*	To demonstrate the fundamental principles of PCM decoding, transforming a serial binary bitstream back into a continuous analog message.
*	To understand the critical role of synchronization, specifically how matching the decoder’s clock (CK) and frame synchronization (FS) to the encoder is essential for preventing data misinterpretation.
*	To observe Digital-to-Analog conversion, specifically how 8-bit binary numbers are mapped to proportional voltage levels ranging from -2V (00000000) to +2V (11111111).
*	To analyze the formation of a Pulse Amplitude Modulation (PAM) signal, which serves as the intermediate step between the raw digital data and the recovered analog waveform.
*	To validate signal reconstruction techniques by using a Tuneable Low-pass Filter to recover both a pure sine wave and human speech from the decoded PAM signal.

---

# III. MATERIALS

| Item | Description |
| :--- | :--- |
| **Trainer Unit** | Emona Telecoms-Trainer 101 (plus power-pack) |
| **Oscilloscope** | Dual channel 20MHz oscilloscope |
| **Leads (Scope)** | Two Emona Telecoms-Trainer 101 oscilloscope leads |
| **Leads (Patch)** | Assorted Emona Telecoms-Trainer 101 patch leads |
| **Headphone** | One set of headphone (stereo)|

---

# IV. EXPERIMENTAL RESULTS

# 1. PART A – Setting up the PCM encoder
To begin the experiment, you must first generate PCM data by setting up a PCM encoder. Start by gathering the required equipment and configuring the oscilloscope according to the standard instructions from Experiment 1. Ensure the oscilloscope's Trigger Source is set to CH1 and the Mode control is in the CH1 position. Finally, locate the PCM Encoder module and toggle its Mode switch to the PCM position.

## 1.1 Experiment Circuit Procedure
The PCM Encoder is clocked by the 100kHz DIGITAL output from the Master Signals module. Its analog input is driven by the Variable DC module’s VDC output.

<img width="538" height="258" alt="e13 1 1" src="https://github.com/user-attachments/assets/25af91aa-ceef-4db8-bdc2-da7dd7042cc8" />

<img width="398" height="256" alt="e13 1 1 1" src="https://github.com/user-attachments/assets/a7514a35-9545-4048-b062-f724b8298a93" />

## OBSERVATION

![e13 1 1 1 1](https://github.com/user-attachments/assets/adcb6a36-2da1-47ad-907f-e5b7dda8bb5d)

The oscilloscope display captures the critical relationship between the digital data and the timing signals required for successful PCM decoding. The yellow trace (Channel 1) represents the Frame Synchronization (FS) signal, which produces a pulse every 80.17µs to mark the exact beginning of each 8-bit binary word. The blue trace (Channel 2) shows the PCM Serial Data stream, where the toggling high and low voltage levels represent the 8-bit binary code corresponding to the analog input from the Variable DC module.
Because the PCM Decoder module is not self-clocking and cannot self-detect frames, these two signals must be perfectly aligned. The FS signal ensures the decoder correctly identifies the first bit of every frame; without this precise synchronization, the 8-bit numbers would be misinterpreted, leading to an incorrect voltage output. In this specific capture, the constant bit pattern in the blue trace confirms that a steady DC voltage is being encoded, resulting in a consistent binary value for every frame processed.


## 1.2 Experiment Circuit Procedure
To transition the experiment, begin by disconnecting the plug from the Variable DCV module’s output. Next, locate the VCO module, set its Range control to the LO position, and rotate the Frequency Adjust control fully counter-clockwise. You must then modify the hardware setup as illustrated in Figure 3, ensuring the PCM Encoder module's input is now connected to the VCO module's SINE output. Because the input signal is now a continuously changing sine wave, you should observe that the PCM DATA output also changes continuously to reflect the fluctuating input voltage.

<img width="533" height="259" alt="ex13 12 1" src="https://github.com/user-attachments/assets/15a2cdeb-6c82-40df-a223-2b73cfc90b5b" />

<img width="393" height="255" alt="e13 12 2" src="https://github.com/user-attachments/assets/5a16a565-fbed-4dc1-8e7d-775c82e7d1ec" />

## OBSERVATION

![e](https://github.com/user-attachments/assets/7c540b83-5752-4a9e-8570-769642646342)

When the Variable DC input is replaced with a sine wave from the VCO module, the oscilloscope captures the dynamic nature of real-time encoding. The top trace (red/yellow depending on the scope) continues to show the Frame Synchronization (FS) pulses, maintaining a steady period of 80.17µs to define the 8-bit boundaries. However, the lower trace representing the PCM DATA no longer displays a static bit pattern; instead, the logic levels shift and toggle constantly.
This continuous variation occurs because the sine wave's voltage is always changing, forcing the encoder to generate a different 8-bit binary number for every new sample frame. As the analog voltage rises and falls, the binary values fluctuate between the minimum and maximum digital limits, reflecting the proportional mapping required for later decoding into a Pulse Amplitude Modulation (PAM) signal.

# 2. PART B – Decoding the PCM data
To begin the decoding phase, return the oscilloscope's Slope control to the "+" position and set the Mode control to CH1. It is important to observe that the decoder operates using "stolen" clock and frame synchronization signals directly from the encoder to ensure proper alignment. Next, adjust the Timebase control to stabilize the display for approximately two cycles of the message signal. Finally, switch the scope's Mode to DUAL to simultaneously view the original message signal and the reconstructed output from the PCM Decoder module.

## 2.1 Experiment Circuit Procedure

<img width="632" height="261" alt="e13 2 1 1" src="https://github.com/user-attachments/assets/44d63c6b-3ef4-420d-938f-0eca34026f75" />

<img width="591" height="297" alt="e13 2 1 2" src="https://github.com/user-attachments/assets/d12d254f-1bb5-47a0-b3a4-a4ccf648f468" />

## OBSERVATION

![e13 2 1 3](https://github.com/user-attachments/assets/a2359cdd-6a26-402f-be62-24cbf721630f)


The oscilloscope output for Part B demonstrates the successful transformation of digital data back into an analog approximation. The red trace (Channel 1) represents the original sine wave message, while the yellow trace (Channel 2) displays the output of the PCM Decoder module. This yellow waveform is a Pulse Amplitude Modulation (PAM) signal, characterized by its "staircase" appearance. This stepped shape occurs because the decoder generates a voltage proportional to the received 8-bit binary number—mapping values between -2V and +2V—and holds that voltage until the next frame is processed. The close alignment between the peaks of the original sine wave and the staircase steps confirms that the "stolen" clock and frame synchronization signals are functioning correctly, allowing the decoder to accurately interpret the timing of the incoming bitstream.


# 3. PART C- Encoding and decoding speech
To transition to encoding and decoding speech, begin by completely removing the Buffer module from the current arrangement while keeping all other existing leads connected. Disconnect the plugs from the VCO module's SINE output and modify the hardware connections as illustrated in Figure 9. By connecting the SPEECH module to the PCM Encoder's input, you can then talk, sing, or hum into the microphone while monitoring the oscilloscope to observe the real-time digital conversion and analog recovery of your voice.

## 3.1 Experiment Circuit Procedure

<img width="643" height="284" alt="e13 3 1 1" src="https://github.com/user-attachments/assets/fc2fabd7-03d8-4f5b-be65-4c600d21603a" />

# OBSERVATION

![e13 3 1 2](https://github.com/user-attachments/assets/9b31949f-76e7-4f71-94d7-c2eaa4297511) ![e13 3 1 3](https://github.com/user-attachments/assets/a7af7461-5288-49b0-b1de-0cf93386dd4b)



When transitioning from a silent state to active speech, the oscilloscope reveals a dramatic shift in the complexity of the encoded and decoded signals. In the left image, where there is no sound, the signals remain relatively stable and uniform, representing the system's baseline or "quiet" state. However, the right image—captured while talking, singing, or humming—shows both the message signal and the decoded output becoming highly irregular and dynamic. The top trace (speech message) displays the complex, non-periodic fluctuations of human vocal cord vibrations, while the bottom trace (PCM Decoder output) exhibits a rapidly changing staircase pattern as it attempts to track these nuances in real-time. This observation confirms that the PCM system successfully responds to the continuously changing analog input by generating a corresponding sequence of unique 8-bit binary frames, which are then reconstructed into a representative, albeit "stepped," version of the original audio.

# 4. PART D- Recovering the message
To finalize the message recovery process, locate the Tuneable Low-pass Filter module, setting its Gain to the middle and its Cut-off Frequency control fully counter-clockwise. After disconnecting the speech module and modifying the setup according to Figure 10, slowly rotate the cut-off frequency control clockwise until the message signal is successfully reconstructed. To verify the recovery through audio, integrate the Buffer module as shown in Figure 12 and use headphones to listen to the filter's output. Finally, by switching the buffer lead between the PCM Decoder and the VCO module outputs, you can confirm that the reconstructed signal and the original source are aurally similar.

## 4.1 Experiment Circuit Procedure

<img width="644" height="265" alt="e14 1 1 1" src="https://github.com/user-attachments/assets/fbbbf2ef-730a-43bd-a835-fdbc72e9abf8" />

<img width="556" height="257" alt="e14 1 1 2" src="https://github.com/user-attachments/assets/e6e849ac-b05f-4a2a-972c-1798936e52ed" />

## OBSERVATION

![e14 1 1 3](https://github.com/user-attachments/assets/12fa770e-e3ad-4813-9abf-b20ae7f2eeba)

The final stage of the experiment demonstrates the successful reconstruction of the message signal from the PCM bitstream using a low-pass filter. As shown in the oscilloscope output, the red trace (Channel 1) represents the original sine wave message, while the yellow trace (Channel 2) captures the signal after it has passed through the Tuneable Low-pass Filter. By rotating the module's Cut-off Frequency control clockwise, the "staircase" levels of the Pulse Amplitude Modulation (PAM) signal are smoothed out, effectively removing the high-frequency quantization noise inherent in the digital-to-analog conversion. Although the reconstructed signal may exhibit a slight phase shift relative to the original, the two waveforms are clearly the same in frequency and shape. This visual confirmation, validated by similar audio results when using the headphones and Buffer module, proves that a low-pass filter can accurately recover a continuous analog signal from discrete PCM data frames.

---

# V. Lab Assessment: Post-Experiment Questions

**Question 1: What does the PCM Decoder's "stepped" output tell you about the type of signal that it is?**

Answer: The "stepped" or staircase nature of the PCM Decoder's output indicates that it is a Pulse Amplitude Modulation (PAM) signal. This appearance tells us that the signal is a discrete-time representation of the original message, where the decoder has recovered specific voltage levels from the 8-bit digital words and held them constant for the duration of each sampling frame.

**Question 2: What must be done to the PCM Decoder module's output to reconstruct the message properly?**

Answer: To reconstruct the message properly, the PCM Decoder’s output must be passed through a Low-pass Filter. This filter removes the high-frequency "switching" noise and sharp edges of the staircase steps, smoothing the transitions to recover the original continuous analog waveform.

**Question 3: Even though the two signals look and sound the same, why isn't the reconstructed message a perfect copy of the original message?**

Answer: The reconstructed message is not a perfect copy due to quantization error. Because the PCM encoder uses a finite number of bits (8 bits in this case) to represent an infinite range of analog voltages, it must "round" the actual voltage to the nearest available digital level. This rounding process creates a slight discrepancy between the original signal and the digital representation, resulting in a permanent loss of detail known as quantization noise.

---

# VI. Conclusion
The experiment successfully demonstrated the end-to-end process of Pulse Code Modulation (PCM) systems, from initial digital encoding to final analog reconstruction. By configuring the PCM Encoder with a 100kHz clock, it was established that precise timing—specifically the Frame Synchronization (FS) signal—is indispensable for decoding; without these "stolen" timing signals to mark the start of each 8-bit word, the serial data would be misinterpreted. Observations across varying inputs, including static DC, dynamic sine waves, and complex speech, proved that the encoder effectively maps fluctuating analog voltages into unique binary frames in real-time.
The decoding phase revealed that the immediate output of a PCM Decoder is a Pulse Amplitude Modulation (PAM) signal, characterized by a "staircase" appearance where discrete voltage levels are held for the duration of each sampling frame. While this signal successfully follows the frequency and envelope of the original message, it contains significant quantization noise and sharp transitions.
The final stage confirmed that the original analog message can be effectively recovered by passing the PAM signal through a Tuneable Low-pass Filter. This filtering process smooths the "steps" of the staircase, removing high-frequency switching noise to produce a continuous waveform that both looks and sounds like the original source. Ultimately, the experiment validates that while quantization introduces minor deviations, the combination of synchronized decoding and low-pass filtering provides a robust method for transmitting and recovering analog information in a digital format.
