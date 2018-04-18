from scipy import fftpack
from matplotlib import pyplot as plt
fp = open('planet.txt', "r")
line = fp.readline()
statistics=[]
while line:
    line = fp.readline()
    line2=line.strip().split()
    #print line2
    #print type(line2)
    for item in line2:
        if float(item) >1:
            statistics.append(float(1.))
        else:
            statistics.append(float(line2[0]))
#print statistics
sig = np.asarray(statistics)
# The FFT of the signal
sig_fft = fftpack.fft(sig)
power = np.abs(sig_fft)

# The corresponding frequencies
time_step = 0.01
period = 0.0014

sample_freq = fftpack.fftfreq(sig.size, d=time_step)

# Plot the FFT power
plt.figure(figsize=(6, 5))
plt.plot(sample_freq, power)
plt.xlabel('Frequency [Day]')
plt.ylabel('plower')

# Find the peak frequency: we can focus on only the positive frequencies

pos_mask = np.where(sample_freq > 0)
freqs = sample_freq[pos_mask]
peak_freq = freqs[power[pos_mask].argmax()]

# Check that it does indeed correspond to the frequency that we generate
# the signal with
np.allclose(peak_freq, 1./period)

plt.figure(figsize=(6, 5))
plt.plot(sig,)
plt.show()
fp.close()
    
print max(sig_fft)
