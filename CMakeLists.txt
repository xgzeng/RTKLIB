cmake_minimum_required(VERSION 3.10)
project(rtklib)

# rtklib
aux_source_directory(src SRCS)
aux_source_directory(src/rcv SRCS_RCV)

add_library(rtklib
  ${SRCS} ${SRCS_RCV})

if (CMAKE_C_COMPILER_ID STREQUAL "AppleClang")
target_compile_definitions(rtklib PRIVATE _DARWIN_C_SOURCE)
endif()

target_include_directories(rtklib PUBLIC "src")

# rtkrvc
add_executable(rtkrcv
    app/rtkrcv/vt.h
    app/rtkrcv/vt.c
    app/rtkrcv/rtkrcv.c
)
target_link_libraries(rtkrcv rtklib)