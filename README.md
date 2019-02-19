# Password Manager with Intel(R) SGX Enclave

## Purpose of the project

The project demonstrates several fundamental usages of Intel(R) Software Guard eXtensions (Intel(R) SGX) SDK :
* Initializing and destroying an enclave
* Creating ECALLs or OCALLs
* Calling trusted libraries inside the enclave


## How to build/execute the application

### Prerequisites

* [Intel(R) SGX SDK for Linux* OS](https:/github.com/intel/linux-sgx)
Make sure your environment is set.
```
$ source /path/to/sgxsdk/environment
```

#### Hardware mode

* [Intel(R) SGX PSW for Linux* OS](https:/github.com/intel/linux-sgx)
* [Intel(R) SGX driver for Linux* OS](https:/github.com/intel/linux-sgx-driver)

### Build and execute

#### Hardware Mode

* Debug build
```
$ make
```
* Pre-release build
```
$ make SGX_PRERELEASE=1 SGX_DEBUG=0
```
* Release build
```
$ make SGX_DEBUG=0
```

#### Simulation Mode

* Debug build
```
$ make SGX_MODE=SIM
```
* Pre-release build
```
$ make SGX_MODE=SIM SGX_PRERELEASE=1 SGX_DEBUG=0
```
* Release build
```
$ make SGX_MODE=SIM SGX_DEBUG=0
```

#### Execute

```
$ ./app
```

#### Extra informations

* If ```sgxsdk``` is not installed in ```/opt``` then add the following while compiling with the Makefile
```
$ make SGX_SDK=/path/to/sgxsdk ...
```
* Remember to clean before switching build mode
```
$ make clean
```

## Configurations Parameters

### Explanation about parameters

#### TCSMaxNum, TCSNum, TCSMinPool

These three parameters will determine whether a thread will be created dynamically when there is no available thread to do the work.

#### StackMinSize, StackMaxSize

For a dynamically created thread, ```StackMinSize``` is the amount of stack available once the thread is created and ```StackMaxSize``` is the total amount of stack that thread can use. The gap between ```StackMinSize``` and ```StackMaxSize``` is the stack dynamically expanded as necessary at runtime.

For a static thread, only ```StackMaxSize``` is relevant which specifies the total amount of stack available for the thread.

#### HeapMaxSize, HeapInitSize, HeapMinSize

```HeapMinSize``` is the amount of heap available once the enclave is initialized.

```HeapMaxSize``` is the total amount of heap an enclave can use. The gap between ```HeapMinSize``` and ```HeapMaxSize``` is the heap dynamically expanded as necessary at runtime.

```HeapInitSize``` is here for compatibility.

### Sample configuration files for the enclave

* config.01.xml : There is no dynamic thread, no dynamic heap expansion.
* config.02.xml : There is no dynamic thread, but dynamic heap expansion can happen.
* config.03.xml : There are dynamic threads. For a dynamic thread, there's no stack expansion.
* config.04.xml : There are dynamic threads. For a dynamic thread, stack will expanded as necessary.
