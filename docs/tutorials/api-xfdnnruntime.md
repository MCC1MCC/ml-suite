# group `xfdnnruntime` 

Provide brief description of the APIs here. What are the apis and why do we need them?

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
createHandle       | Programs a hardware acceleration engine to the FPGA, and initializes communication.
closeHandle       | Terminates communication by destroying handle.
initScript       | Loads the network schedule on the hardware accelerator.
execute       | Executes inference on the hardware accelerator.
exec_async       | Executes inference on the hardware accelerator.
get_result       | Get result of execution for a given PE, and a given stream.
computeSoftmax       | Compute the softmax of a given activation or a set of activations.
processCommandLine       | Invoke command line parser for command line deployment flows.
printClassification       | Print the result of classification given class scores, and a synset labels file.
loadWeights_samePE       | Load weights to off chip device memory.
loadWeights       | Load weights to off chip device memory.
prepareInput       | Allocate memory for inputs, load images from disk, images will be scaled, letteboxed, and preprocessed.
prepareOutput       | Allocate memory for outputs.

## Members

### `public def `[`createHandle`](#group__xfdnnruntime_1gaeed72e652dc4a62fe3126e930ae4e6bd)`(xclbin,kernel,libFile,numHandles,deviceID)`

Programs a hardware acceleration engine to the FPGA, and initializes communication.

#### Parameters
* `xclbin` [str] Path to binary image (a.k.a. xclbin) to be loaded. 

* `kernel` [str] Name of kernel in xclbin. Always use "kernelSxdnn_0". To be deprecated. 

* `libFile` [str] Path to libxfdnn.so shared library. This is the high performance middleware invoked by the Python APIs. 

* `numHandles` [int] Number of handles to be created. This parameter is reserved for future development.

#### Returns
* `int` Return Code 

* `0` For success

### `public def `[`closeHandle`](#group__xfdnnruntime_1ga97c95fb46ba89c653c8926834abaf11f)`()`

Terminates communication by destroying handle.

No return value.

### `public def `[`initScript`](#group__xfdnnruntime_1gae88de7311e8b8fb21dcd1a8ba1350fce)`(netFile,weightsBlob,numBatches,cfgFile,scale,PE,streamId)`

Loads the network schedule on the hardware accelerator.

This API call is blocking.

#### Parameters
* `netFile` [str] Path to file which contains network specific instructions, this file should be generated by xfdnn compiler. 

* `weightsBlob` [<class 'xdnn.LP_c_short'>] This is an object constructed by the xdnn_io.loadWeights API, which provides the address in memory where weights preside. 

* `numBatches` [int] Number of images to process per execute call. 

* `cfgFile` [str] Path to file which contains network specific quantization parameters, this file should be generated by xfdnn quantizer. 

* `scale` [int] Scale used for bias terms in global quantization mode, typically set to 30. 

* `PE` [int] Index used to target specific processing element. Use -1 for autoselect. There can be from 1 to 6 processing elements in a particular xclbin. 

* `streamId` [int] Argument not required.

### `public def `[`execute`](#group__xfdnnruntime_1ga54d228620c6ab03f911e79d520d416e1)`(netFile,weightsBlob,inputs,output,numBatches,cfgFile,scale,PE,streamId)`

Executes inference on the hardware accelerator.

This API call is blocking.

#### Parameters
* `netFile` [str] Path to file which contains network specific instructions, this file should be generated by xfdnn compiler. 

* `weightsBlob` [<class 'xdnn.LP_c_short'>] This is an object constructed by the xdnn_io.loadWeights API, which provides the address in memory where weights preside. 

* `inputs` [<class 'xdnn.LP_c_short_Array_1'>] Array holding the input volume for which to run inference. This object is constructed by the xdnn_io.prepareInput API. 

* `outputs` [numpy.ndarray] Array holding the result of the inference ran on the hardware accelerator. Shape will be (fpgaoutsz,) where fpgaoutsz is the total number of elements in the final activation ran in HW. 

* `numBatches` [int] Number of images to process per execute call. 

* `cfgFile` [str] Path to file which contains network specific quantization parameters, this file should be generated by xfdnn quantizer. 

* `scale` [int] Scale used for bias terms in global quantization mode, typically set to 30. 

* `PE` [int] Index used to target specific processing element. Use -1 for autoselect. There can be from 1 to 6 processing elements in a particular xclbin. 

* `streamId` [int] Argument not required.

#### Returns
* `int` Return Code 

* `0` for success

### `public def `[`exec_async`](#group__xfdnnruntime_1ga95ee7688fcfbdabd5e25e753e335246d)`(netFile,weightsBlob,inputs,output,numBatches,cfgFile,scale,PE,streamId)`

Executes inference on the hardware accelerator.

This API call is non-blocking. The result of execution can be fetched using xdnn.get_result.

#### Parameters
* `netFile` [str] Path to file which contains network specific instructions, this file should be generated by xfdnn compiler. 

* `weightsBlob` [<class 'xdnn.LP_c_short'>] This is an object constructed by the xdnn_io.loadWeights API, which provides the address in memory where weights preside. 

* `inputs` [<class 'xdnn.LP_c_short_Array_1'>] Array holding the input volume for which to run inference. This object is constructed by the xdnn_io.prepareInput API. 

* `outputs` [numpy.ndarray] Array holding the result of the inference ran on the hardware accelerator. Shape will be (fpgaoutsz,) where fpgaoutsz is the total number of elements in the final activation ran in HW. 

* `numBatches` [int] Number of images to process per execute call. 

* `cfgFile` [str] Path to file which contains network specific quantization parameters, this file should be generated by xfdnn quantizer. 

* `scale` [int] Scale used for bias terms in global quantization mode, typically set to 30. 

* `PE` [int] Index used to target specific processing element. Use -1 for autoselect. There can be from 1 to 6 processing elements in a particular xclbin. 

* `streamId` [int] Stream ID used to recover result at a later time.

#### Returns
* `int` Return Code 

* `0` for success

### `public def `[`get_result`](#group__xfdnnruntime_1ga442f4d9fff3f6d295260c7a432662631)`(PE,streamId)`

Get result of execution for a given PE, and a given stream.

This API is used in conjuntion with xdnn.exec_async.

#### Parameters
* `PE` [int] Index used to target specific processing element. Use -1 for autoselect. There can be from 1 to 6 processing elements in a particular xclbin. 

* `streamId` [int] Stream ID to recover result from.

#### Returns
* `int` Return Code 

* `0` for success

### `public def `[`computeSoftmax`](#group__xfdnnruntime_1ga14c379362e8dc4d904d89566b4e8f4fe)`(data,num)`

Compute the softmax of a given activation or a set of activations.

#### Parameters
* `data` [numpy.ndarray] Activation or a set of activations corresponding to multiple images stored as a 1D Array. 

* `num` [int] Number of images processed.

#### Returns
* `numpy.ndarray` Softmax Activation

### `public def `[`processCommandLine`](#group__xfdnnruntime_1gad1b09a4aa61dd2000ec26a702753780b)`(argv)`

Invoke command line parser for command line deployment flows.

### `public def `[`printClassification`](#group__xfdnnruntime_1gab39439a4389260daae18365073ba3151)`(output,args)`

Print the result of classification given class scores, and a synset labels file.

#### Parameters
* `output` [numpy.ndarray] Class scores, typically the output of the softmax layer. 

* `args` [dict] Collection of arguments. Most importanly args["labels"] which is the path to a file containing class names.

### `public def `[`loadWeights_samePE`](#group__xfdnnruntime_1gab26481603753867cfa3c98e8e8f2dbad)`(args)`

Load weights to off chip device memory.

The weights are first quantized.

#### Parameters
* `args` [dict] Collection of arguments. Most importanly args["datadir"] which is the path to a folder containing weights & biases.

#### Returns
* `tuple`  (weightsBlob, fcWeight, fcBias)  <class 'xdnn.LP_c_short'>, numpy.ndarray, numpy.ndarray

### `public def `[`loadWeights`](#group__xfdnnruntime_1gaf5c32ea13a0fced300d155f446e2e5bd)`(args)`

Load weights to off chip device memory.

The weights are first quantized.

#### Parameters
* `args` [dict] Collection of arguments. Most importanly args["datadir"] which is the path to a folder containing weights & biases.

#### Returns
* `tuple`  (weightsBlob, fcWeight, fcBias)  <class 'xdnn.LP_c_short'>, numpy.ndarray, numpy.ndarray

### `public def `[`prepareInput`](#group__xfdnnruntime_1gaa0033a27d75cc85dbb062cbc2a48a469)`(args,PE)`

Allocate memory for inputs, load images from disk, images will be scaled, letteboxed, and preprocessed.

#### Parameters
* `args` [dict] Collection of arguments. Most importanly args["images"] which is a list of images to prepare. 

* `PE` [int] Index used to target specific processing element. Use -1 for autoselect. There can be from 1 to 6 processing elements in a particular xclbin.

#### Returns
* `tuple`  (fpgaInputs,batch_sz)  <class 'xdnn.LP_c_short_Array_1'>, int

### `public def `[`prepareOutput`](#group__xfdnnruntime_1gad7909f65f26996db8b10243337cdf297)`(output_sz,batch_sz)`

Allocate memory for outputs.

#### Parameters
* `output_sz` [int] Number of elements in the output volume returned by FPGA for a single inference. This is specific to the network. 

* `batch_sz` [int] Number of images to be processed simultaneously.

#### Returns
* `numpy.ndarray` 1D Array large enough to hold output_sz*batch_sz elements.
