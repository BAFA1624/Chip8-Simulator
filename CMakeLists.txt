cmake_minimum_required(VERSION 3.30.5)

project(Chip8-Emulator)

# CMake Includes
include(CTest)

# Compiler Stuff
if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(CMAKE_CXX_COMPILER /opt/homebrew/bin/g++-13)
endif()

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_FLAGS_DEBUG "-fopenmp -fconcepts-diagnostics-depth=3 -Wall -Wextra -Wconversion -pedantic -O0 -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "-fopenmp -Wno-error=deprecated-declarations -Wno-error=maybe-uninitialized -Wno-error=deprecated-enum-enum-conversion -Wno-error=class-memaccess -Werror -DNDEBUG -march=native -Wall -Wextra -pedantic -O3")

include_directories(./include/)
add_subdirectory(src)

