cmake_minimum_required(VERSION 4.0)

project(restinio_template_project VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 26)

include(cmake/CMakeLists.txt)

if(NOT DEFINED BOOST_ROOT)
    set(BOOST_ROOT "${CMAKE_INSTALL_PREFIX}")
endif()

get_package(Catch2 Catch2::Catch2)
get_package(expected-lite nonstd::expected-lite)
get_package(fmt fmt::fmt)
get_package(llhttp llhttp::llhttp_static)
get_package(restinio restinio::restinio)
get_library(sqlite3)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    get_package(Catch2 Catch2::Catch2WithMain)
    file(GLOB ALL_SOURCES src/*.cpp tests/*.cpp)
else ()
    file(GLOB ALL_SOURCES src/*.cpp src/main/main.cpp)
endif ()

include_directories(${CMAKE_SOURCE_DIR}/include)

make_executable("${PROJECT_NAME}")

install(TARGETS "${PROJECT_NAME}")