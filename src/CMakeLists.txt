include_directories(../include/)

set(sources chip8.cpp)

message(STATUS "Creating Chip8 shared library...")
add_library(Chip8 SHARED ${sources})
set(LINK_LIBS ${LINK_LIBS} Chip8 PARENT_SCOPE)
