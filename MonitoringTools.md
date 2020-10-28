## Cloud monitoring tools

### Overview 

#### Linux monitoring tools 
##### CPU monitoring 
1. sar - part of the sysstat package. You can monitor
   * can be used for collective CPU usage and individual CPU statistics
   * Memory used, availabl;e, swap space 
   * Overall I/O and individual I/O activities
   * Average data loads and run queueus
   * Example: 
   * <pre><code>sar 1,3</code></pre>
2. top - displays all the running process in the system ordered by certain columns. 
usage - <pre><code>top -hv | -bcHisS -d delay -n limit -u|U user | -p pid -w [cols]</code></pre>
<pre><code>top -p $PID | grep docker</code></pre>
batch mode operation - could be useful for sending output from top to other programs or to a file
<pre><code>top -b -n limit</code></pre>
3. htop - Interactive tool like top commands. (Perform a yum install) 
<pre><code>sudo yum install htop -y</code></pre>
Iostat - CPU, disk I/O and NFS stats 
<pre><code>iostat
iostat -p sda
Linux 5.4.17-2011.7.4.el7uek.x86_64 (k8s-node-1-ad2)    10/28/2020      _x86_64_        (56 CPU)
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.05    0.00    0.06    0.00    0.00   99.89
Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               2.21        12.33        16.91     860968    1181064
sda2              0.00         0.06         0.00       4356          0
sda3              2.21        12.20        16.91     852116    1181064
sda1              0.00         0.03         0.00       2212          0</code></pre>
5. mpstat - CPU code stats
<pre><code>mpstat -I ALL -u -P ALL
11:43:39 AM  CPU       HI/s    TIMER/s   NET_TX/s   NET_RX/s    BLOCK/s IRQ_POLL/s  TASKLET/s    SCHED/s  HRTIMER/s      RCU/s
11:43:39 AM    0       0.00      14.58       0.00       0.20       0.00       0.00       0.01      18.98       0.00      10.85
11:43:39 AM    1       0.00      11.52       0.00       0.01       0.01       0.00       0.00       5.89       0.00       8.22
11:43:39 AM    2       0.00      10.90       0.00       3.63       1.23       0.00       0.07       4.99       0.00       7.45
11:43:39 AM    3       0.00      12.06       0.18       0.00       0.00       0.00       0.00       6.04       0.00       8.71</code></pre>
6. vmstat - reports virtual memory statistics. displays memory usage (including swap)
<pre><code>vmstat</code></pre>
[More examples](https://www.thegeekstuff.com/2011/07/iostat-vmstat-mpstat-examples/)

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
