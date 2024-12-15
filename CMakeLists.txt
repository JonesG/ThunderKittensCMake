cmake_minimum_required(VERSION 2.8)

project(kittens_tests LANGUAGES CUDA CXX)

set(CMAKE_CXX_STANDARD 20)

add_executable( kittens_tests
                ${PROJECT_SOURCE_DIR}/tests/unit/unit_tests.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/warp.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/memory.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/tile/tile.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/tile/global_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/tile/global_to_shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/tile/shared_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/vec/vec.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/vec/global_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/vec/global_to_shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/memory/vec/shared_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/tile/tile.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/tile/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/tile/reductions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/tile/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/tile/mma.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/vec/vec.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/vec/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/vec/reductions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/register/vec/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/tile/tile.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/vec/vec.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/tile/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/tile/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/tile/reductions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/vec/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/vec/reductions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/warp/shared/vec/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/group.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/memory.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/tile/tile.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/vec/vec.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/tile/tile.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/tile/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/tile/reductions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/tile/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/vec/vec.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/vec/maps.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/shared/vec/conversions.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/tile/global_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/tile/global_to_shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/tile/shared_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/vec/global_to_register.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/vec/global_to_shared.cu
                ${PROJECT_SOURCE_DIR}/tests/unit/group/memory/vec/shared_to_register.cu
)

target_compile_options(kittens_tests PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:
                        --expt-relaxed-constexpr
                       >)

# #include "intellisense_cuda_intrinsics.h"

                      
set(CMAKE_VS_SDK_INCLUDE_DIRECTORIES
    "${PROJECT_SOURCE_DIR}/include";
    "${PROJECT_SOURCE_DIR}/tests/unit";
    "${PROJECT_SOURCE_DIR}/tests/unit/testing_commons")

add_compile_definitions( KITTENS_4090 )

target_compile_definitions(kittens_tests PUBLIC
                            TEST_ALL )

target_include_directories( kittens_tests PUBLIC
                            "${PROJECT_SOURCE_DIR}/include"
                            "${PROJECT_SOURCE_DIR}/tests/unit"
                            "${PROJECT_SOURCE_DIR}/tests/unit/testing_commons" )

set_property(TARGET kittens_tests PROPERTY CUDA_ARCHITECTURES native)
