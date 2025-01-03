# NETRA-DATA-PACKET
 Comprehensive Signal Analysis: Time-Domain and Frequency-Domain Techniques for Signal Processing on netra_50msps.dat


### Detailed Summary of Signal Processing Workflow for **Netra_50MSPS.dat**

This repository contains a detailed workflow for analyzing and processing a complex time-domain signal sampled at **50 MSPS**. The signal undergoes multiple stages of analysis and processing, including visualization, frequency offset correction, filtering, resampling, and feature extraction. The following sections provide a breakdown of the methodology and insights.

---

### **1. Load and Visualize the Original Signal**  
The input data is a complex signal stored in a `.dat` file, representing time-domain samples. 

- **File format**: Binary `.dat` file.  
- **Sampling rate**: 50 MSPS (Mega Samples Per Second).  
- **Number of samples**: 3330.  
- **Signal duration**: 6.66e-05 seconds.

#### **Time-Domain Representation**  
The amplitude of the signal is plotted over time to visualize its behavior.  
- **X-axis**: Time (in seconds).  
- **Y-axis**: Amplitude of the signal.  
- This plot provides an intuitive understanding of the signal’s variations over time.

---

### **2. Spectrogram of the Original Signal**  
A spectrogram provides a **time-frequency representation** of the signal, showing how its frequency content evolves over time.  
- **X-axis**: Time (seconds).  
- **Y-axis**: Frequency (Hz).  
- **Color intensity**: Power in decibels (dB), representing the signal's energy at each time-frequency point.  

This representation is essential for identifying time-varying characteristics and dominant frequency components.

---

### **3. Frequency Spectrum Analysis**  
The **Fast Fourier Transform (FFT)** is used to compute the signal’s frequency spectrum.  
- **FFT size**: 2048.  
- **FFT shift**: Applied to center zero frequency.  
- **Plot description**:
  - **X-axis**: Frequency (Hz).  
  - **Y-axis**: Magnitude of the frequency components.  

The spectrum highlights the presence of dominant frequencies in the signal, providing insights into its spectral content before correction.

---

### **4. Frequency Offset Estimation and Correction**  
Frequency offset refers to a constant shift in the signal’s carrier frequency, which can occur due to hardware imperfections or environmental factors.

#### **Offset Estimation**  
- **Detected offset frequency**: 1.94 MHz.  
- This offset is identified by analyzing the frequency spectrum and pinpointing the deviation of the peak frequency from the expected center.

#### **Offset Correction**  
- The correction involves multiplying the signal with a **complex exponential**:  
  \[
  \text{Corrected Signal} = \text{Original Signal} \cdot e^{-j 2 \pi \text{Offset Frequency} \cdot t}
  \]
- **Result**: The frequency components are realigned to their proper positions.

#### **Post-Correction Spectrogram**  
A spectrogram of the offset-corrected signal is plotted to confirm the alignment of frequency components.

---

### **5. Low-Pass Filtering**  
A low-pass filter is applied to limit the signal’s frequency content to a desired range.  

#### **Filter Details**  
- **Filter type**: Butterworth low-pass filter.  
- **Cutoff frequency**: 4.5 MHz.  

#### **Implementation**  
- The filter is designed using `scipy.signal.butter`, and the filtered signal is obtained using `scipy.signal.sosfiltfilt`.  

#### **Output**  
- **Filtered Signal**: A spectrogram and frequency spectrum are plotted to verify the removal of high-frequency components.  

---

### **6. Resampling**  
Resampling adjusts the sampling rate of the signal while preserving its time duration.

#### **Details**  
- **Original sampling rate**: 50 MSPS.  
- **Resampled rate**: 11 MSPS.  
- **Implementation**: Resampling is performed using `scipy.signal.resample`.  

#### **Output**  
- The resampled signal is visualized to confirm the successful downsampling process.

---

### **7. Power Spectral Density (PSD) Analysis**  
The **Power Spectral Density (PSD)** quantifies the distribution of signal power across frequencies.  

#### **Method**  
- **Technique**: Welch’s method.  
- **Window**: Hamming window.  
- **Output**:  
  - **X-axis**: Frequency (MHz).  
  - **Y-axis**: Power in dB/Hz.  

#### **Purpose**  
- Identify noise characteristics in specific frequency bands.  
- Analyze the power distribution of the signal.  

---

### **8. Magnitude and Phase Response**  
The FFT of the signal is used to compute:  
- **Magnitude Spectrum**: Represents the signal’s strength across frequencies.  
- **Phase Spectrum**: Shows the phase shift introduced at each frequency.  

Plots are generated for both the original and processed signals, with frequency expressed in MHz.

---

### **9. Feature Extraction**  
Key signal features are extracted from both the time and frequency domains.

#### **Time-Domain Features**  
- Minimum amplitude: 0.0070.  
- Maximum amplitude: 0.4552.  
- Mean value: 0.2828.  
- RMS value: 0.2941.  
- Variance: 0.0065.  
- Peak-to-peak amplitude: 0.4482.  
- Crest factor: 1.5479.  
- Skewness: -0.7647.  
- Kurtosis: 0.0573.  

#### **Frequency-Domain Features**  
- Maximum frequency component power: 6.22e-05.  
- Total power: 0.0865.  
- Average power: 2.60e-05.  
- Frequency domain variance: 1.55e-10.  
- Skewness: -0.1214.  
- Kurtosis: -0.7593.  

---

### **10. Bandwidth Calculation**  
The total bandwidth of the signal is calculated as:  
\[
\text{Total Bandwidth} = 2 \times \text{Cutoff Frequency}
\]  
For a cutoff frequency of 4.5 MHz, the bandwidth is **9 MHz**.

---

### **11. Signal-to-Noise Ratio (SNR)**  
The SNR of the filtered signal is computed to evaluate signal quality.  
- **SNR**: 13.78 dB.

---
