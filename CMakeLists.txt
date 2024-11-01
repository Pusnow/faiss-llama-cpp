cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 17)

project(faiss-llama-cpp)

add_executable(fl src/main.cpp)

include(cmake/CPM.cmake)
cpmaddpackage(
  GITHUB_REPOSITORY
  jarro2783/cxxopts
  VERSION
  3.2.0
  OPTIONS
  "CXXOPTS_BUILD_EXAMPLES NO"
  "CXXOPTS_BUILD_TESTS NO"
  "CXXOPTS_ENABLE_INSTALL YES")
target_link_libraries(fl PRIVATE cxxopts)

cpmaddpackage(
  GITHUB_REPOSITORY
  facebookresearch/faiss
  VERSION
  1.9.0
  OPTIONS
  "FAISS_ENABLE_GPU NO"
  "FAISS_ENABLE_PYTHON NO"
  "FAISS_ENABLE_C_API NO"
  "FAISS_OPT_LEVEL generic"
  "BUILD_TESTING NO")
target_link_libraries(fl PRIVATE faiss)

cpmaddpackage(
  GITHUB_REPOSITORY
  ggerganov/llama.cpp
  GIT_TAG
  b4002
  OPTIONS
  "LLAMA_BUILD_TESTS NO"
  "LLAMA_BUILD_EXAMPLES NO"
  "LLAMA_BUILD_SERVER NO")
target_link_libraries(fl PRIVATE llama)
