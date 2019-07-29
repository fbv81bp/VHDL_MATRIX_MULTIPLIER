# VHDL_MATRIX_MULTIPLIER
Generic description of a pipelined matrix multiplier with 4 multiplier threads. It calculates  C += A * B'

The core operates on 3 BRAMs stroring the input matrices A, B and the initial values of C. It uses all ports of BRAMs which makes 4 parallely running multiplications possible. So two lines of matrix A and two columns of matrix B are being siultaneously accesses and multiply accumlated to result in 4 cells of matrix C. The accumlators are initiated by the original 4 values of C that are getting later on updated.

The calculation of C += A * B' enables multiplying larger matrices by partitioning them into ones that fit into the FPGA and calculate different areas of C separatly. This algorithm requires the accumlation of consecutively calculated sub-matrices of C.

The design structure is pipelined to bring out the most of the Xilinx Artix structure, and would be capable of running at 300MHz, but the control structure's addressing limits this to 250MHz.

In the future the controls addressing, which is the bottleneck, will be able to be improved if wider data buses will be used. In this case the above 300MHz may be reachable. Furthermore if DSP primitives get instantiated instead of leaving it the synthesizer, then the control signal to OPMODE input path may be registered: the synthesizer seems not to recognize an additional register on this path as the internal register of the DSP block. Thus in case parameterized DSP primitives are being used, the theroetical limit of 450MHz might be reached.
