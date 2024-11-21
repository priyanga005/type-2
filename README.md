import numpy as np
from scipy import signal
import matplotlib.pyplot as plt

# Filter specifications
fsample = 1000  # Sampling rate (Hz)
fp = 100  # Passband frequency (Hz)
fs = 200  # Stopband frequency (Hz)
Ap = 1  # Passband ripple (dB)
As = 40  # Stopband attenuation (dB)

# Normalize the frequencies (by Nyquist frequency)
wp = 2 * fp / fsample  # Normalized passband frequency
ws = 2 * fs / fsample  # Normalized stopband frequency

# Design Chebyshev Type II filter
order, wn = signal.cheby2(N=4, rs=As, Wn=ws, btype='low', analog=False, output='ba', fs=fsample)

# Frequency response
w, h = signal.freqz(order, wn, worN=2000)

# Plot frequency response
plt.plot(w * fsample / (2 * np.pi), abs(h), 'b')
plt.plot(fp, 0.5 * np.sqrt(0.5), 'ko')
plt.axvline(fp, color='k')
plt.axvline(fs, color='k')
plt.xlim(0, 0.5 * fsample)
plt.title("Chebyshev Type II Frequency Response")
plt.xlabel('Frequency [Hz]')
plt.ylabel('Amplitude')
plt.grid()
plt.show()
