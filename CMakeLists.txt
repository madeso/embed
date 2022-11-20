cmake_minimum_required(VERSION 3.15)

if(NOT DEFINED EMBED_MASTER_PROJECT)
    set(EMBED_MASTER_PROJECT OFF)
    if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
        set(EMBED_MASTER_PROJECT ON)
    endif()
endif()
message(STATUS "Embed master: ${EMBED_MASTER_PROJECT}")

if(EMBED_MASTER_PROJECT)
    set_property(GLOBAL PROPERTY USE_FOLDERS OFF)
endif()

# project(embed C CXX)
# set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")

include(cmake/StandardProjectSettings.cmake)
include(cmake/CompilerWarnings.cmake)
include(cmake/Sanitizers.cmake)

add_library(embed_project_options INTERFACE)
add_library(embed_project_warnings INTERFACE)

target_compile_features(embed_project_options INTERFACE cxx_std_17)
set_project_warnings(embed_project_warnings)
enable_sanitizers(embed_project_options)

add_subdirectory(tools)
add_subdirectory(src)
