---
layout: ../../layouts/BlogPost.astro
title: Bicyclic Matrix-Matrix Multiplication in Fully Homomorphic Encryption

---
In an earlier article, I covered the basic technique for performing matrix-vector multiplication in fully homomorphic encryption (FHE), known as the Halevi-Shoup diagonal method. This article covers a more recent method for matrix-matrix multiplication known as the bicyclic method.

The code implementing this method is in the same GitHub repository as the previous article, and the bicyclic method is in a file called bicyclic.py.

The previous article linked above covers the general concepts behind “FHE packing,” which I will assume as background knowledge for this article:

The “abstract” computational model of SIMD-style FHE (CKKS, BGV, BFV) involving ciphertexts represented as large-width vectors of slots, with elementwise additions, multiplications, and rotations as elementary operations.
The conjoined duties of packing data into ciphertexts (akin to memory layout) and deciding what circuit of elementary operations operates on that packing to implement the functionality equivalent to the desired cleartext operation.
The efficiency metrics: small multiplicative depth, few rotation operations, and the ability to batch rotations on the same ciphertext (hoisting).
The bicyclic method
The bicyclic method was introduced in the paper Homomorphic Matrix Operations under Bicyclic Encoding by Jingwei Chen, Linhan Yang, Wenyuan Wu, Yang Liu, and Yong Feng. I first heard about it via an extension of the technique to support batch matrix-matrix multiplication in Tricycle: Private Transformer Inference with Tricyclic Encodings by Lawrence Lim, Vikas Kalagi, Divyakant Agrawal, and Amr El Abbadi.

The technique also involves a diagonal-like packing similar to the Halevi-Shoup method, and as a result it enjoys many of the same benefits:

- A minimal multiplicative depth of 1.
- Layout-invariant, meaning the output is packed according to the same algorithm as the input   (modulo differences in matrix dimensions).
- A number of rotations that scales linearly with the matrix dimension, though lower-level tricks (Baby-Step-Giant-Step, for another post) reduce that to more like a square-root growth.

``` python
import numpy as np

for i in range(x):
    print(i + 2)

## This should print all the numbers from 1 to 10
```

``` php
return [
    'listeners' => [
        WorkerStarting::class => [                                      
            EnsureUploadedFilesAreValid::class,                         
        ],

        RequestReceived::class => [                                     
            ...Octane::prepareApplicationForNextOperation(),            
            ...Octane::prepareApplicationForNextRequest(),              
        ],

        WorkerErrorOccurred::class => [                                 
            ReportException::class,                                     
            StopWorkerIfNecessary::class,                               
        ],
    ],

    'warm' => [
        ...Octane::defaultServicesToWarm(),                             
    ],
]
```