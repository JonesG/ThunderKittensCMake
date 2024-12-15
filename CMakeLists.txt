cmake_minimum_required(VERSION 3.5)

project(kittens_tests LANGUAGES CUDA CXX)

set(CMAKE_CXX_STANDARD 20)

cmake_path(SET THUNDERKITTENS_ROOT "${PROJECT_SOURCE_DIR}/modules/ThunderKittens" )
cmake_path(SET THUNDERKITTENS_UNIT_TEST_ROOT "${THUNDERKITTENS_ROOT}/tests/unit" )

add_executable( kittens_tests
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/unit_tests.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/warp.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/memory.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/tile/tile.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/tile/global_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/tile/global_to_shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/tile/shared_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/vec/vec.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/vec/global_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/vec/global_to_shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/memory/vec/shared_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/tile/tile.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/tile/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/tile/reductions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/tile/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/tile/mma.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/vec/vec.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/vec/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/vec/reductions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/register/vec/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/tile/tile.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/vec/vec.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/tile/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/tile/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/tile/reductions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/vec/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/vec/reductions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/warp/shared/vec/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/group.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/memory.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/tile/tile.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/vec/vec.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/tile/tile.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/tile/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/tile/reductions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/tile/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/vec/vec.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/vec/maps.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/shared/vec/conversions.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/tile/global_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/tile/global_to_shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/tile/shared_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/vec/global_to_register.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/vec/global_to_shared.cu
                ${THUNDERKITTENS_UNIT_TEST_ROOT}/group/memory/vec/shared_to_register.cu
)

target_compile_options(kittens_tests PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:
                        --expt-relaxed-constexpr
                       >)

# #include "intellisense_cuda_intrinsics.h"

                      
set(CMAKE_VS_SDK_INCLUDE_DIRECTORIES
    "${THUNDERKITTENS_ROOT}/include"
    "THUNDERKITTENS_UNIT_TEST_ROOT"
    "${THUNDERKITTENS_UNIT_TEST_ROOT}/testing_commons")

add_compile_definitions( KITTENS_4090 )

target_compile_definitions(kittens_tests PUBLIC
                            TEST_ALL )

target_include_directories( kittens_tests PUBLIC
                            "${THUNDERKITTENS_ROOT}/include"
                            "THUNDERKITTENS_UNIT_TEST_ROOT"
                            "${THUNDERKITTENS_UNIT_TEST_ROOT}/testing_commons" )

set_property(TARGET kittens_tests PROPERTY CUDA_ARCHITECTURES native)
