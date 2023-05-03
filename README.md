Download Link: https://assignmentchef.com/product/solved-cs1550-project3-virtual-memory-simulator
<br>
In class, we have been discussing various page replacement algorithms that an Operating System implementer may choose to use. In this project, you will compare the results of three different algorithms on traces of memory references. While simulating an algorithm, you will collect statistics about its performance, such as the number of page faults that occur and the number of dirty frames that had to be written back to disk. When you are done with your program, you will write up your results and provide a graph that compares the performance of the various algorithms.

The three algorithms for this project are:

<strong>OPT</strong> – Simulate what the optimal page replacement algorithm would choose if it had perfect knowledge

<strong>Least Recently Used (LRU)</strong>– Simulate least recently used, whereby you will track when pages were last accessed and evict the least recently used page.

<strong>Second Chance Algorithm </strong>– Candidate pages are considered for removal in a round robin manner, and a page that has been accessed between consecutive page faults will not be evicted. The page will be replaced if it has not been accessed since its last consideration. That is, each page gets a “second chance” before it is replaced. In the worst case, if the second chance bit is set for all pages, the bit is cleared and second chance algorithm degenerates to FIFO.

You may write your program in C/C++, Java, Perl, or Python as long as it runs on thoth.cs.pitt.edu.

Implement a page table for a <strong>32-bit</strong> address space. All pages will be <strong>4KB</strong> in size. The number of frames will be a <strong>parameter</strong> to the execution of your program.

<h1><a name="_Toc5107"></a>Project Details</h1>




You will write a program called vmsim that takes the following command line arguments:

./vmsim –n &lt;numframes&gt; -a &lt;opt|lru|second&gt; &lt;tracefile&gt;

The program will then run through the memory references of the file and decide the action taken for each address (hit, page fault – no eviction, page fault – evict clean, page fault – evict dirty).

When the trace is over, print out summary statistics in the following format:

Algorithm: LRU

Number of frames:       8

Total memory accesses:  %d

Total page faults:      %d

Total writes to disk:   %d




<h2><a name="_Toc5108"></a>Implementation</h2>

We are providing three sample memory traces. The traces are available at /u/OSLab/original/ in the files gzip.trace.gz, swim.trace.gz, and gcc.trace.gz. We will use more trace files to test your program.

Each trace is gzip compressed, so you will have to copy each trace to your directory under /u/OSLab/USERNAME/ and then decompress it like:

gunzip bzip.trace.gz

Your simulator takes a command-line argument that specifies the trace file that will be used to compute the output statistics. The trace file will specify all the data memory accesses that occur in the sample program. Each line in the trace file will specify a new memory reference. Each line in the trace will therefore have the following two fields:

<strong>Access Type:</strong> A single character indicating whether the access is a load (‘l’) or a store (‘s’). The ‘s’ mode modifies the address and sets the dirty bit to true.

<strong>Address:</strong> A 32-bit integer (in unsigned hexadecimal format) specifying the memory address that is being accessed. For example, “0xff32e100” specifies that memory address 4281524480 (in decimal) is accessed.

Fields on the same line are separated by a single space. Example trace lines look like:

l 0x300088a0 s 0x1ffffd00




If you are writing in C, you may parse each line with the following code:

unsigned int address; char mode;

fscanf(file, “%c %x”, &amp;mode, &amp;addr);

<h2><a name="_Toc5109"></a>Important Notes</h2>

<ol>

 <li>Evicting a page happens by identifying the page to evict and writing the page to the disk (if dirty), or abandoning the page (if clean).</li>

 <li>Implementing OPT in a naïve fashion will lead to unacceptable performance. It should not take more than <strong>5 minutes</strong> to run your program.</li>

 <li>In case of a tie, in the OPT algorithm, break the tie by selecting the least recently used page. If you are using Python, name your file vmsim and add the following shebang line at the beginning of the file: #!/usr/bin/env python</li>

</ol>

<h2><a name="_Toc5110"></a>Write Up</h2>

<strong>Part 1:</strong> For each of your three algorithm implementations, describe in a document the resulting page fault statistics for <strong>8, 16, 32, and 64 frames</strong>. Use this information to determine which algorithm you think might be most appropriate for use in an actual operating system. Use OPT as the baseline for your comparisons.

<strong>Part 3:</strong> For Second Chance, with the three traces and varying the total number of frames from 2 to 100, determine if there are any instances of Belady’s anomaly. Discuss in your writeup.

<strong>Part 3</strong>: Discuss the implementation and runtime of the OPT algorithm

<h2><a name="_Toc5111"></a>File Backups</h2>




One of the major contributions the university provides for the AFS filesystem is nightly backups. However, the /u/OSLab/ partition on thoth is not part of AFS space. Thus, any files you modify under your personal directory in /u/OSLab/ are not backed up. If there is a catastrophic disk failure, all of your work will be irrecoverably lost. As such, it is my recommendation that you:

<a href="#_ftnref1" name="_ftn1">[1]</a> Based upon Project 3 of Dr. Misurda’s CS 1550 course.