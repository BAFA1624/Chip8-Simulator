cmake_minimum_required(VERSION 3.30.5)

project(Chip8-Emulator)

# CMake Includes
include(CTest)

# Requried Packages
find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

# Compiler Stuff
if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(CMAKE_CXX_COMPILER /opt/homebrew/Cellar/gcc/14.2.0_1/bin/g++-14)
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 23)

#set(LINK_LIBS)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)

# Setting default compiler flags
set(CMAKE_CXX_FLAGS_DEBUG "-Wall -Wextra -Wconversion -pedantic -O0 -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "-Werror -DNDEBUG -march=native -Wall -Wextra -pedantic -O3")

include_directories(./include/ ${OPENGL_INCLUDE_DIRS} ${GLUT_INCLUDE_DIRS})
add_subdirectory(src)

add_executable(main src/main.cpp)
add_custom_command(
	TARGET main POST_BUILD
	COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_BINARY_DIR}/compile_commands.json ${CMAKE_SOURCE_DIR}/compile_commands.json
	COMMENT "Transferring compile_commands.json"
)
target_link_libraries(main PRIVATE ${LINK_LIBS})
