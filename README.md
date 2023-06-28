# Quantum-Hadamard-Edge-detection
A Quantum Algorithm for Image edge detection utilizing the principles of Quantum Computing and Quantum Parallelism and Hadamard Gate
------------------------------------------------------------------------------------------------------------------------------------
Implementation Objectives:
1.To implement Quantum edge detection for a 8x8 binary image array.
2.To implement Quantum edge detection for a 32x32 binary image array.
3.To implement Quantum edge detection for a 32x32 RGB image array

code Implementation details:

The edge detection algorithm aims to identify the boundaries or edges of objects
within an image. The algorithm consists of the following steps:
1. Load and Pre-process the Image using QPIE:
we used Pillow library to open and resize images and then converted the image into
a numpy array with intensity values. Then we use a technique called Quantum
Probability Image Encoding to encode the intensities of each pixel into coefficients of
quantum states. For this we first normalize the intensity values and convert them to
coefficients of quantum states(see fig.4.1) . The quantum state can be represented as
shown in (fig.4.2).
2. Define Quantum Circuits and QHED Algorithm - Then we create quantum
circuits to perform horizontal and vertical scans. - for an MxN image pixels we
require logbase2(M XN ) data qubits. so for a 8x8 image we require 6 data-qubits
and for a 32x32 image we require 10 data qubits. we also need 1 ancillary qubit in
additional. it works as padding for the image and helps avoid errors. so total qubits
= data-qubits +1. we create a unitary matrix of size dXd where d is the number of
data qubits needed. then we shift it to the right one step column wise. this gives
our decrement gate (also called as amplitude permutation unitary gate) (see fig 4.4)
. this is used to identify image gradients. The first step in our circuit is to put all
states in superposition. so we apply H gate to all the qubits (fig. 4.3). Then we apply
Decrement gate to this image state. This transforms the image state to as shown in
fig.4.5. we see that the even positions of this state are the values of image gradients
between adjacent pixels. This is what we are looking for.
4. Horizontal Scan: - Measure the qubits at the even positions and compare them
with threshold. we used the threshold as < 1e − 15 or > 1e + 15. if the gradient value
falls in threshold region we update it as 1, else no edge so 0. This way we obtain
Horizontal scan edges..
5. Vertical Scan: we take the transpose of image matrix and perform all the steps
till applying Decrement gate. after this we measure the image state at even positions
using threshold as < 1e − 15 or > 1e + 15. This way we obtain vertical scan edges.
6. Combine Scan Results: - Combine the results of the horizontal and vertical
scans using OR Logical gate to obtain the final edge-detected image.


