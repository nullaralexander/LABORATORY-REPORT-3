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
