cmake_minimum_required(VERSION 3.0)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

project(hello)

include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
conan_basic_setup()

include(os)

set(SOURCES
  main.cpp
)

find_library(v8 v8_monolith ${CMAKE_CURRENT_SOURCE_DIR}/deps/v8/v8/out.gn/x64.release.sample/obj)

os_add_executable(hello "Hello world - OS included" ${SOURCES})

#os_include_directories(hello
#  PUBLIC
#    ${CMAKE_CURRENT_SOURCE_DIR}/deps/v8/v8/include
#)

os_add_stdout(hello default_stdout)

os_link_libraries(hello
  ${v8}
)
