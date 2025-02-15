#
# Copyright (c) 2020-2021, NVIDIA CORPORATION.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

################################################################################
# Add executable: tiff_image
################################################################################

add_executable(tiff_image tiff_image/main.cpp)
set_source_files_properties(tiff_image/main.cpp PROPERTIES LANGUAGE CUDA)

set_target_properties(tiff_image
    PROPERTIES
        CXX_STANDARD 17
        CXX_STANDARD_REQUIRED YES
        CXX_EXTENSIONS NO
        CUDA_STANDARD 17
        CUDA_STANDARD_REQUIRED YES
        CUDA_EXTENSIONS NO
        CUDA_SEPARABLE_COMPILATION ON
        CUDA_RUNTIME_LIBRARY Shared
)
target_compile_features(tiff_image PRIVATE ${CUCIM_REQUIRED_FEATURES})
# Use generator expression to avoid `nvcc fatal   : Value '-std=c++17' is not defined for option 'Werror'`
target_compile_options(tiff_image PRIVATE $<$<COMPILE_LANGUAGE:CXX>:-Werror -Wall -Wextra>)
target_link_libraries(tiff_image
        PRIVATE
            ${CUCIM_PACKAGE_NAME}
            deps::fmt
        )
