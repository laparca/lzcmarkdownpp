cmake_minimum_required(VERSION 3.10)
project(lzcmarkdownpp VERSION 0.1)

include(cmake/CPM.cmake)
CPMAddPackage(
    NAME cmark-gfm
    GITHUB_REPOSITORY github/cmark-gfm
    GIT_TAG 0.29.0.gfm.9
    OPTIONS
      "CMARK_STATIC On"
      "CMARK_SHARED Off"
      "CMARK_TESTS Off"
    )

#set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_LIST_DIR}")
#find_package(CMark REQUIRED)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_library(lzcmarkdownpp src/markdown.cc)
target_include_directories(lzcmarkdownpp
    PUBLIC
        $<INSTALL_INTERFACE:include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    PRIVATE
        ${cmark-gfm_SOURCE_DIR}/src
        ${cmark-gfm_BINARY_DIR}/src
        "${CMAKE_CURRENT_SOURCE_DIR}/src"
)

#add_executable(markdown_test src/main.cc)
#target_link_libraries(lzcmarkdownpp ${CMARK_LIBRARY})
target_link_libraries(lzcmarkdownpp libcmark-gfm_static)
