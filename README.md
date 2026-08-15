This is a modified triton-windows used for turing(sm75). Baed on triton-windows-3.7.1.post27 from https://github.com/triton-lang/triton-windows. Unlock int8mma and int4mma on turing card. Int4mma code is planted from this repo https://github.com/Chennesxu/triton-turing.
Integer GEMM — INT4 doubles INT8, and cuBLAS has no INT4 path
<img width="640" height="480" alt="Figure_1" src="https://github.com/user-attachments/assets/47aa7d67-d94b-4b86-8cab-3dec7d4a2805" />
INT4 (m8n8k32) reaches ≈ 2× the throughput of INT8 (peak 219 TOPS), gaining on both fronts: 2× Tensor Core compute and half the shared-memory traffic (operands stay packed as int32). cuBLAS exposes no INT4 GEMM at all on Turing — this is the first usable pure-int4 matmul in Triton (upstream marks the path "Not implemented"). Triton INT8 also clears cuBLAS INT8 by ~1.8×.
You can down load source code and build in MSVC.
1.Open x64 Native Tools Command Prompt for VS 2022 cmd window
2.cd triton-windows-turing
3.python setup.py bdist_wheel -v
4.afer building complete,you'll get a .whl file in dist folder.
5.pip install ****.whl
6.python testint8int4.py,you'll get int8 and int4 mma test and benchmark result. py file below

