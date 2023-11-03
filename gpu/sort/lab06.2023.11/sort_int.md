## Summary
to sort 200M integers, gpu is ~4x faster than cpu
```
% ./k11
2023-11-03 14:00:08 6core 15gb avx2 Linux gpu(NVIDIA GeForce GTX 1080 Ti) 0.11 test
 l:200000000?200000000
 \a
"gpu enabled"
 \t lg:^:l
4680
 \a -g
 \a
"gpu not enabled"
 \t lc:^:l
17013
 lg~lc
1b
```
## interesting results
- `% ./k11 is.200M.k` shows ~4x speedup
- `% ./k11 is.100M.k` shows 2.56x speedup
- `% ./k11 is.80M.k` shows 2.21x speedup
- `% ./k11 is.50M.k` shows 0.9x speedup, so GPU is slower than CPU
- `% ./k11 is.10M.k` shows 0.9x speedup, so GPU is slower than CPU
## some conclusions:
- GPU works better with bigger data(100M+)
- when big data size doubles(e.g. 100M to 200M, time grows from 3.284s to 4.615s), only 1.5x time more

## hw configs:
### cpu:
```
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         46 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  6
  On-line CPU(s) list:   0-5
Vendor ID:               GenuineIntel
  Model name:            Intel(R) Xeon(R) CPU E5-2603 v4 @ 1.70GHz
    CPU family:          6
    Model:               79
    Thread(s) per core:  1
    Core(s) per socket:  6
    Socket(s):           1
    Stepping:            1
    CPU max MHz:         1700.0000
    CPU min MHz:         1200.0000
    BogoMIPS:            3395.94
```
### gpu:
```
   0  NVIDIA GeForce GTX 1080 Ti      Off   00000000:02:00.0 Off                   N/A 
  23%   28C    P8                9W / 250W      2MiB / 11264MiB       0%      Default
```
