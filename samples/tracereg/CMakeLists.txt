CMAKE_MINIMUM_REQUIRED(VERSION 3.10)
PROJECT(tracereg LANGUAGES C CXX)

SET(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

INCLUDE_DIRECTORIES("${CMAKE_CURRENT_LIST_DIR}/../syelog")

FILE(GLOB src
    ${CMAKE_CURRENT_LIST_DIR}/*.cpp
	${CMAKE_CURRENT_LIST_DIR}/*.rc
)

# TODO: Is there any smart way to find Win32 Standard Libraries?
# It is Visual C++ Compiler only way.
# For MinGW or Clang based compilers, it should not work.
SET(CMAKE_CXX_STANDARD_LIBRARIES
    "${CMAKE_CXX_STANDARD_LIBRARIES} advapi32.lib")

ADD_LIBRARY(tracereg SHARED ${src})
TARGET_LINK_LIBRARIES(tracereg PUBLIC detours_static)
TARGET_LINK_LIBRARIES(tracereg PUBLIC syelog)

TARGET_COMPILE_DEFINITIONS(tracereg PUBLIC ${DETOURS_COMPILE_DEFINITIONS})
TARGET_COMPILE_OPTIONS(tracereg PUBLIC ${DETOURS_COMPILE_OPTIONS})