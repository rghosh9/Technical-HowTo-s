## Cloud monitoring tools

### Overview 

#### Linux monitoring tools 
##### CPU monitoring 
1. sar - part of the sysstat package. You can monitor
top 
<pre><code>top -p $PID | grep docker</code></pre>
htop - to install in RHEL/Oracle install 
<pre><code>sudo yum install htop -y</code></pre>

##### Memory monitoring 
<pre><code>mpstat -p all</code></pre>
<pre><code>vmstat</code></pre> 
most important entries are 
1. free - amount of memory available 
2. si - paged(swapped) in
3. so - paged(swapped) out 
##### Disk subsystem monitoring 
<pre><code>iostat -x /dev/sda
Linux 2.6.32-220.el6.x86_64 (tramp) 04/17/2012 _x86_64_ (2 CPU)
avg-cpu: %user %nice %system %iowait %steal %idle
6.44 0.00 1.99 4.35 0.00 87.22
Device: rrqm/s wrqm/s r/s w/s rsec/s wsec/s avgrq-sz avgqu-sz await svctm %util
sda 0.05 1.92 0.13 0.92 4.98 21.44 25.25 0.07 67.53 30.49 3.19</code></pre>

#### Telemetry monitoring tools 

#### CPU / GPU Monitoring tools 
1. [NVIDIA-smi](https://developer.nvidia.com/nvidia-system-management-interface) 
The NVIDIA System Management Interface (nvidia-smi) is a command line utility, based on top of the [NVIDIA Management Library (NVML)](https://developer.nvidia.com/nvidia-management-library-nvml), intended to aid in the management and monitoring of NVIDIA GPU devices.
NVIDIA-smi ships with NVIDIA GPU display drivers on Linux, and with 64bit Windows Server 2008 R2 and Windows 7. Nvidia-smi can report query information as XML or human readable plain text to either standard output or a file. 
[NVIDIA-smi documentation](http://developer.download.nvidia.com/compute/DCGM/docs/nvidia-smi-367.38.pdf)
2. [NVIDIA-smi docker container]()

#### Recording monitoring history 

Reference links
1. [Testing NVIDIA-smi with docker](https://learning.oreilly.com/library/view/generative-adversarial-networks/9781789139907/66f7aba5-465e-4958-a2c6-55319edf12c1.xhtml) 
2. [monitis blog](https://www.monitis.com/blog/key-linux-performance-metrics/)
