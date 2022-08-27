# Building with custom CUDA_PATH and Compute Capability
```
cd gpu-burn
make COMPUTE=<compute capability value> CUDAPATH=/usr/local/cuda-<version>
```
Check **compute capability** for nvidia gpu: https://en.wikipedia.org/wiki/CUDA
|GPU|CC|
|--|--|
|Tesla V100,|7.0|
|A100 80GB, A100 40GB| 8.0|

# GPU Stress Test
```
./gpu_burn -d <num_seconds>
```


# gpu-burn
Multi-GPU CUDA stress test
http://wili.cc/blog/gpu-burn.html

# Easy docker build and run

```
git clone https://github.com/wilicc/gpu-burn
cd gpu-burn
docker build -t gpu_burn .
docker run --rm --gpus all gpu_burn
```

# Building
To build GPU Burn:

`make`

To remove artifacts built by GPU Burn:

`make clean`

GPU Burn builds with a default Compute Capability of 5.0.
To override this with a different value:

`make COMPUTE=<compute capability value>` 

CFLAGS can be added when invoking make to add to the default
list of compiler flags:

`make CFLAGS=-Wall`

LDFLAGS can be added when invoking make to add to the default
list of linker flags:

`make LDFLAGS=-lmylib`

NVCCFLAGS can be added when invoking make to add to the default
list of nvcc flags:

`make NVCCFLAGS=-ccbin <path to host compiler>`

CUDAPATH can be added to point to a non standard install or
specific version of the cuda toolkit (default is 
/usr/local/cuda):

`make CUDAPATH=/usr/local/cuda-<version>`

CCPATH can be specified to point to a specific gcc (default is
/usr/bin):

`make CCPATH=/usr/local/bin`

# Usage

    GPU Burn
    Usage: gpu_burn [OPTIONS] [TIME]
    
    -d	Use doubles
    -tc	Use Tensor cores
    -h	Show this help message
    
    Example:
    gpu_burn -d 3600
    
## Example
```bash
cd gpu-burn
make COMPUTE=7.0 CUDAPATH=/usr/local/cuda-11.0

while :
do
  ./gpu_burn -d 180
  sleep 1800
done

sleep 10h
```
