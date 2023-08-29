cmake_minimum_required (VERSION 3.17 FATAL_ERROR)
set (CMAKE_CXX_STANDARD 17)
project(OnnxTest
VERSION 0.0.0
LANGUAGES CXX
DESCRIPTION "Onnx Runtime Testing Library")

add_executable(HelloOnnx)

target_sources(HelloOnnx PRIVATE main.cpp)

add_library (onnxruntime SHARED IMPORTED)
set_target_properties (onnxruntime PROPERTIES IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/onnxruntime/build/MacOS/RelWithDebInfo/libonnxruntime.1.16.0.dylib)

target_link_libraries(HelloOnnx PRIVATE onnxruntime)

set_target_properties(
    HelloOnnx PROPERTIES
    VERSION "${PROJECT_VERSION}"
    SOVERSION "${PROJECT_VERSION_MAJOR}"
)


# this was from a post from someone on discord showing how they had linked the static parts of the Onnx runtime build,
# ideally a static build would be ideal, like : https://github.com/olilarkin/ort-builder 
# but I have no been able to get that to compile yet

# cmake -B Builds , makes a  folder called Builds in directory, and creates build files
# then you can cd into Builds folder, and do make HelloOnnx

# set(ONNX_RUNTIME_DEPS
#     ${CMAKE_CURRENT_BINARY_DIR}/onnxruntime/build/${CMAKE_BUILD_TYPE}/_deps
#     # ${CMAKE_CURRENT_BINARY_DIR}/onnxruntime/build/MacOS/RelWithDebInfo/_deps
# )
# set(ONNX_RUNTIME_LINK_DIRS
#     ${CMAKE_CURRENT_BINARY_DIR}/onnxruntime/build/MacOS/RelWithDebInfo/lib
#     ${ONNX_RUNTIME_DEPS}/protobuf-build
#     ${ONNX_RUNTIME_DEPS}/onnx-build
#     ${ONNX_RUNTIME_DEPS}/re2-build
#     ${ONNX_RUNTIME_DEPS}/abseil_cpp-build/absl/base
#     ${ONNX_RUNTIME_DEPS}/abseil_cpp-build/absl/container
#     ${ONNX_RUNTIME_DEPS}/abseil_cpp-build/absl/hash
#     ${ONNX_RUNTIME_DEPS}/google_nsync-build
#     ${ONNX_RUNTIME_DEPS}/pytorch_cpuinfo-build
#     ${ONNX_RUNTIME_DEPS}/pytorch_cpuinfo-build/deps/clog
# )
# set(ONNX_RUNTIME_LIBS
#     # onnxruntime itself
#     onnxruntime_session
#     onnxruntime_optimizer
#     onnxruntime_providers
#     onnxruntime_util
#     onnxruntime_framework
#     onnxruntime_graph
#     onnxruntime_mlas
#     onnxruntime_common
#     onnxruntime_flatbuffers
#     # dependencies
#     absl_base
#     absl_throw_delegate
#     absl_raw_hash_set
#     absl_hash
#     absl_city
#     absl_low_level_hash
#     onnx
#     onnx_proto
#     protobuf-lite$<$<CONFIG:Debug>:d>
#     nsync_cpp
#     cpuinfo
#     clog
#     re2
#     # misc
#     $<$<NOT:$<STREQUAL:${CMAKE_SYSTEM_NAME},Android>>:pthread>
#     $<$<STREQUAL:${CMAKE_SYSTEM_NAME},Android>:log>
#     dl
# )
# onnxruntime is the namespace

# link_directories(${CMAKE_BINARY_DIR}/onnxruntime/build/MacOS/RelWithDebInfo/build)





