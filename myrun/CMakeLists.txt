cmake_minimum_required(VERSION 3.16)

project(myrun LANGUAGES C CXX VERSION 0.0.0.0)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3")

set(MYRUN_HEADER_FILE ${CMAKE_BINARY_DIR}/include_temp/binary_data.h)
# set(MYRUN_EMBED_FILE ${CMAKE_CURRENT_SOURCE_DIR}/../buildroot/output/images/Image)
set(MYRUN_EMBED_FILE ${CMAKE_CURRENT_SOURCE_DIR}/../baremetal/baremetal.bin)
set(MYRUN_ARGUMENTS -m 0x6000000)

add_subdirectory(bintoh++)
add_subdirectory(rv32ima)