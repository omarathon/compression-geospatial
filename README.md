## Cambridge MRes Project:<br>"Assessing high-performance lightweight compression formats for Geospatial computation"

### Files

Core codecs implemented in the `codecs` directory.

Main programs:
* `test_comp.cpp`: test codecs
* `bench_comp.cpp`: benchmark codecs
* `bench_pipeline.cpp`: benchmark geospatial pipelines

Additional files:
* `test_remappings.cpp`: verifies Morton remappings
* `util.h`, `transformations.h`, `remappings.h`: CPP utilities
* `py/*`: Python utilities

### Setup (Basic)
1. obtain the submodules in `external` and build them
2. `make`

### Setup (Fusing Summing into Decompression)
1. Re-build `external/FastPFor` and `external/simdcomp` from these forks:
    1. FastPFor: https://github.com/omarathon/FastPFor
    1. simdcomp: https://github.com/omarathon/simdcomp
1. Replace `codecs/custom_vec_logic_codecs.h` with `agg/custom_vec_logic_codecs.h` (the new file contains the modification to the `custom_rle_vecavx512` codec which fuses summing into decompression)
1. Replace `bench_pipeline.cpp` with `agg/bench_pipeline.cpp`
1. `make clean && make`

### Setup (Running on HPC)
1. `source hpc/modules.sh`
2. Replace `Makefile` with `hpc/Makefile` (the new Makefile contains compiler modifications for the HPC)
3. `make`
