covert-channels
===============

Covert channels are channels in which the transfer of communication is possible, although the channels do not exist explicitly for this purpose. In a computer, these channels exist due to contention over a shared resource between two processes. These channels even extend to complex processes, such as virtual machines. To construct a channel, the two VM's (receiver and sender) must first agree on the period length for communication and the time within the period that each VM will contend for the resource. Second, the VM's synchronize their clocks to achieve high bandwidths. Once synchronized, the VM's are then able to carry out communication. Lastly, the traces are processed offline and the discrete waveform collected by the receiver is translated into a binary signal. Please view the Wiki page for more details on this process.

This repository contains two scripts for communicating across a the L1 cache covert channel. Currently, the code works for the Ubuntu operating system. 

readerL1.cpp - This script runs the receiving end of the L1 cache channel. The program requires the PAPI library in order to poll performance counters for the hit rate of the L1 cache and the dlib package to processes the trace. The channel waits until the starting time (about once every 4 seconds), and then begins the PRIME-ACCESS-PROBE communication across the channel. After the trace has been collected, it is processed with the dlib machine learning library, and every data point is classified as a 0 or 1. 

senderL1.cpp - This script runs the sending end of the L1 cache channel. The program first creates a random 10,000 bit signal that is sent to the receiving program. It then waits until the starting time (about once every 4 seconds), and begins the PRIME-ACCESS-PROBE communication across the channel. It either makes heavy accesses to the L1 cache to communicate a 1, or idles to communicate a 0.
