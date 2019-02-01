# pyVBAN
python implementation of the VBAN (VB Audio network) protocol
Specification here: https://www.vb-audio.com/Voicemeeter/VBANProtocol_Specifications.pdf

pyVBAN.VBAN_Recv() usage:
```python
cl = VBAN_Recv("IP-FROM","StreamName",Port,OutputDeviceIndex,verbose=False)
cl.runforever()
```

Example:
```python
cl = VBAN_Recv("127.0.0.1","Stream7",6981,10,verbose=False)
cl.runforever()
```
or

```python
cl = VBAN_Recv("127.0.0.1","Stream7",6981,10,verbose=False)
while True:
	cl.runonce()
```
To find the output device index you can use this code:

```python
import pyaudio
p = pyaudio.PyAudio()
info = p.get_host_api_info_by_index(0)
numdevices = info.get('deviceCount')

print "--- INPUT DEVICES ---"
for i in range(0, numdevices):
        if (p.get_device_info_by_host_api_device_index(0, i).get('maxInputChannels')) > 0:
            print "Input Device id ", i, " - ", p.get_device_info_by_host_api_device_index(0, i).get('name')
            
print "--- OUTPUT DEVICES ---"
for i in range(0, numdevices):
        if (p.get_device_info_by_host_api_device_index(0, i).get('maxOutputChannels')) > 0:
            print "Input Device id ", i, " - ", p.get_device_info_by_host_api_device_index(0, i).get('name')
```