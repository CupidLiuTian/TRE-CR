# TRE-CR

## Contents

  [1. Introduction](#1-introduction)<br>
  [2. Overview](#1-overview)  
  [3. Contribution process](#2-contribution-process)  
  [4. Compile and Run](#3-compile-and-run)  
  [5. Contact](#4-contact)

## 1.Introduction
 
This is an enhanced DMTCP(https://github.com/dmtcp/dmtcp.git) plugin to checkpoint- restart CUDA and MPI application with noval split-process architecture, it is developed upon CRAC(https://github.com/DMTCP-CRAC/CRAC-early-development) and MANA(https://github.com/mpickpt/mana). The Plugin code contains two part:1)CUDA plugin, the code is in the contrib/trecr-cuda_interceptor directory, 2)MPI plugin, the code is in the contrib/trecr-mpi_interceptor. <br>

The main contribution of TRE-CR:<br>
GMMU - GPU Memory Management Unit(contrib/trecr-cuda_interceptor/lh/mmu)<br>
Incremental and Compression checkpoint - Increatal(contrib/trecr-cuda_interceptor/lh/increamental) and Compression(contrib/trecr-cuda_interceptor/uh)<br>
NCCL application support<br>

## 2. Overview

MANA transparently checkpoints MPI application, CRAC transparently checkpoints CUDA application. In order to transparently checkpoints MPI based CUDA application, a new solution is designed called TRE-CR, this 
is an efficient and time-saving checkpointing and restore mechanism. In compared with CRAC or DMTCP, we additionly support some new features and fix some bugs, detailed change point can refer to changelog-TRE-CR.txt.

## 3. Contribution process

Researchers and Individuals who want to contribute to the project is recommanded refer to the following steps : 

```
git clone https://github.com/SAITPublic/TRE-CR.git
cd TRE-CR
git remote add origin https://github.com/SAITPublic/TRE-CR.git
git branch -M main
git add *.source file
git commit *.source file
git push -uf origin main
```

## 4. Compile and Run

For compile and simple test the TRE-CR for checkpointing and restore GPU applications, we recommand the following steps : 

### 4.1 Compile

```
cd TRE-CR/
./configure
make
cd TRE-CR/contrib/trecr-mpi_interceptor
make
make install
cd TRE-CR/contrib/trecr-cuda_interceptor
make
```

After compiled finished, users can generate a bin/ diretory under TRE-CR/ which contains binary execution file for launch, restart et al and kernel-loader, cuda-plugin file under TRE-CR/contrib/trecr-cuda_interceptor/ directory.

### 4.2 Run

For running the TRE-CR with simple GPU applications, we provide a sample for reference : 

```
Step 1:
Start coordinator:
$ <trecr_dir>/bin/trecr_coordinator –port 7790
Step 2:
Open a new terminal, and start demo application:
$<trecr_dir>/contrib/trecr-cuda_interceptor/trecrproxy.exe –target-ld <libc2.31 dir>/lib/ld-linuxx86-64.so.2 –with-plugin <trecr_dir>/contrib/trecr-cuda_interceptor/libcuda-interceptor.so -j <sample_dir>/simpleIPC
```

## Contact

* Tian Liu (tian01.liu@samsung.com)
* Biao Xing (biao.xing@samsung.com)
* Fengtao Xie (fengtao.xie@samsung.com)
* Huiru Deng (huiru.deng@samsung.com)
