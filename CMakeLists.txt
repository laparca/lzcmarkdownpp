cmake_minimum_required(VERSION 3.10)
project(lzcmarkdownpp VERSION 0.1)

include(cmake/CPM.cmake)
CPMAddPackage(
    NAME cmark-gfm
    GITHUB_REPOSITORY github/cmark-gfm
    GIT_TAG 0.29.0.gfm.0
    OPTIONS
      "CMARK_STATIC On"
    )

#set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_LIST_DIR}")
#find_package(CMark REQUIRED)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_library(lzcmarkdownpp src/markdown.cc)
target_include_directories(lzcmarkdownpp PUBLIC ${CMARK_INCLUDE_DIRS} ${CMAKE_CURRENT_LIST_DIR}/src)
#add_executable(markdown_test src/main.cc)
#target_link_libraries(lzcmarkdownpp ${CMARK_LIBRARY})
target_link_libraries(lzcmarkdownpp libcmark-gfm)
