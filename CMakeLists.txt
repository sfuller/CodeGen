cmake_minimum_required(VERSION 3.12)

# https://cmake.org/cmake/help/latest/policy/CMP0077.html
# option() honors normal variables.
if (POLICY CMP0077)
    cmake_policy(SET CMP0077 NEW)
endif()

project(codegen VERSION 0.1.0)

find_package(Python3 COMPONENTS Interpreter REQUIRED)

add_library(codegen INTERFACE)

target_compile_definitions(
    codegen
    INTERFACE
        WITH_CODEGEN
)

target_include_directories(
    codegen
    INTERFACE
        # Add source include files to target's interface include directories for projects using add_subdirectory()
        $<BUILD_INTERFACE:${codegen_SOURCE_DIR}/include>
)

# Include module functions for the parent project as well
include(cmake/Modules/codegen.cmake)
