cmake_minimum_required(VERSION 3.27)
project(myplugin)
set(CMAKE_CXX_STANDARD 17)

# fetch sdk
include(FetchContent)
FetchContent_Declare(
        IdaCmake
        GIT_REPOSITORY "https://github.com/cauldronloader/ida-cmake.git"
        GIT_TAG "e262b4ba0dad3151ac1d7dbf58aebbe5e8ab4760"
)
FetchContent_Declare(
        IdaSdk
        GIT_REPOSITORY "https://github.com/HexRaysSA/ida-sdk.git"
        GIT_TAG "v9.2"
)
FetchContent_MakeAvailable(IdaCmake IdaSdk)

# setup ida sdk and ida cmake
set(IDASDK ${idasdk_SOURCE_DIR}/src)
include(${idacmake_SOURCE_DIR}/idasdkConfig.cmake)

# use ida cmake like how you would in the no-bootstrap template
ida_add_plugin(myplugin
    SOURCES
        main.cpp
    DEBUG_ARGS
        "-t -z10000"
)
