---
name: ISSUE TEMPLATE
about: Bug and Feature Report

---

Before you open an issue, please make sure you have tried the following steps:

1. Make sure your **environment** is the same with (https://mace.readthedocs.io/en/latest/installation/env_requirement.html).
2. Have you ever read the document for your usage?
3. Check if your issue appears in [HOW-TO-DEBUG](https://mace.readthedocs.io/en/latest/development/how_to_debug.html) or [FAQ](https://mace.readthedocs.io/en/latest/faq.html).
4. The form below must be filled.

------------------------

### System information
- **OS Platform and Distribution (e.g., Linux Ubuntu 16.04)**:
- **NDK version(e.g., 15c)**:
- **GCC version(if compiling for host, e.g., 5.4.0)**:
- **MACE version (Use the command: git describe --long --tags)**:
- **Python version(2.7)**: 
- **Bazel version (e.g., 0.13.0)**:

### Model deploy file (*.yml)
library_name: yolo-v3
target_abis: [armeabi-v7a]
model_graph_format: file
model_data_format: file
models:
  yolo_v3:
    platform: tensorflow
    model_file_path: http://cnbj1.fds.api.xiaomi.com/mace/miai-models/yolo-v3/yolo-v3.pb
    model_sha256_checksum: cbdd9a23588a42af95cf510e458f4decc3b1c0a3d6d6ab22e2b4f3d43ff961aa
    subgraphs:
      - input_tensors:
          - input_1:0
        input_shapes:
          - 1,416,416,3
        output_tensors:
          - conv2d_59/BiasAdd:0
          - conv2d_67/BiasAdd:0
          - conv2d_75/BiasAdd:0
        output_shapes:
          - 1,13,13,255
          - 1,26,26,255
          - 1,52,52,255
    runtime: cpu+gpu
    limit_opencl_kernel_time: 0
    nnlib_graph_mode: 0
    obfuscate: 0
    winograd: 0

### Describe the problem
First I converted the yolo-v3.yml to MACE model then I am trying to convert build MACE to library(Step No.-4 in the MACE Documentation) but I am getting issue, I installed all the essential libraries with recommended versions as per the documentation, Please help me to find out this problem.

### To Reproduce
Steps to reproduce the problem:
bash tools/bazel-build-standalone-lib.sh

### Error information / logs
Please include the **full** log and/or traceback here.
build shared lib for armeabi-v7a + cpu_gpu_dsp
ERROR: /home/sahil/mace/mace/codegen/BUILD.bazel:24:1: no such target '@local_version_config//:gen/version': target 'gen/version' not declared in package '' defined by /home/sahil/.cache/bazel/_bazel_sahil/79354786563d3ac70073ed6107e3f80d/external/local_version_config/BUILD.bazel and referenced by '//mace/codegen:mace_version_gen'
ERROR: Analysis of target '//mace/libmace:libmace_dynamic' failed; build aborted: Analysis failed
INFO: Elapsed time: 1.991s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (0 packages loaded)


### Additional context
Add any other context about the problem here, e.g., what you have modified about the code.
