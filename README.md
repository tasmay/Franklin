# Franklin
Franklin's Leader Election Algorithm in play. (C++, OpenMPI)

This readme is intended to be a precise reference/guide for my implementation of Franklin’s Leader Election algorithm for distributed systems. It includes the following sections:

A. Algorithm Overview
B. Tools/Libraries Used
C. Code
D. Steps to Configure the Run Time Environment for the Code
E. Demo Video
_____________________________________________________________________________________

A. Algorithm Overview
---------------------

Franklin’s algorithm is for processes arranged in an undirected ring. Each node has a unique identity. Each node is either active or passive (relay mode) at a given time. The algorithm executes as follows:

– Each active node sends its identity to its neighbours.
– Let each active node p1 receive identities from p0 and p2. Where p0 and p2 are its either neighbours in the ring.
– If min( ID[p0], ID[p2] ) > ID[p1], then p1 becomes passive
– If min( ID[p0], ID[p2] ) < ID[p1], then p1 sends its ID to its neighbours again
– If min( ID[p0], ID[p2] ) == ID[p1], then p1 declares itself as leader
– Passive nodes only pass on messages.
– The loop continues until a leader with highest unique ID has been elected.

![alt tag](https://www.dropbox.com/s/haa6s2kohbyrkte/franklin.png?dl=0)

See the above image. Considering the topology in Figure 1. the processes are connected in a ring with their unique identifiers as shown. After the first round, processes with ID 0, 1 and 2 become relays as they are the smallest in the immediate neighbourhood.
Figure 1. Figure 2. Figure 3. Figure 4.
In the second round, process with ID 3 enter relay mode as it is the smallest in its neighbourhood. Likewise, in the third round process with ID 4 becomes a relay, leaving only process with ID 5 who
discovers that the IDs received from both of its neighbours belong to itself therefore it then declares itself as the leader.

B. Tools/Libraries Used
-----------------------

I used OpenMPI library for the implementation of this algorithm. OpenMPI is a Message Passing Interface library project used to write portable message-passing programs for parallel and distributed computers. “It can be used in communication for distributed-memory and shared-memory multiprocessors, networks of workstations, and a combination of these elements.”
I tested this code in two ways: (See Section D for details on setting up the run time environment)

1. On my single node machine of 2 GHz Pentium Dual-Core processor using Microsoft Visual Studio as my run-time environment. (Windows OS, VC++ compiler )
2. On a 4-node Virtual Machine MPI cluster over VMware workstation. The nodes read their copy of the parallel code from a shared NFS directory on the master node. (Ubuntu 12.04 LTS, GCC compiler)

C. Code
-------

See Franklin.cpp in the submission package for the code.

D. Steps to Configure the Run Time Environment
----------------------------------------------

This section is two-fold. We can either configure our single node Windows machine to run MPI programs or we can set up a Beowulf OpenMPI cluster comprising of multiple nodes.

To Configure a Single Node Windows Machine:

In order to configure a single node windows machine for OpenMPI, I followed the steps mentioned in the following URL: http://www.eternalthought.co.za/?p=137
Also, one might need to add OpenMPI’s lib and include directories’ path and other library files to the VC++ project configurations in Visual Studio in order to compile the code.

To Setup a Beowulf MPI Cluster on Multiple Linux Nodes:

A step by step tutorial is available here: http://techtinkering.com/2009/12/02/setting-up-a-beowulf-cluster-using-open-mpi-on-linux/

Note: There are slight differences in the VC++ and GCC compiler so there may be cross-compiler compatibility issues when running the same C++ code over the two compilers. This can be resolved with a bit of tinkering here and there.

E. Demo Video
-------------

The above mentioned configuration steps are a bit involved and time consuming. Hence I have prepared a short demo video that shows Franklin’s leader election algorithm in running on my configured cluster. Please see the attached Demo.mp4 file in the submission package.
