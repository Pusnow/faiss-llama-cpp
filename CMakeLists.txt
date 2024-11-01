cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(faiss-llama-cpp)

add_executable(fl src/main.cpp)

include(cmake/CPM.cmake)
