cmake_minimum_required(VERSION 3.28)
project(StackAndQueue C CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(SOURCES
  src/main.cpp
  src/benchmarks/benchmark_base.cpp
)

set(INCLUDE_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR}/../../../external/concurrentqueue
  ${CMAKE_CURRENT_SOURCE_DIR}/../../../external/readerwriterqueue
  ${CMAKE_CURRENT_SOURCE_DIR}/src/include/benchmarks
  ${CMAKE_CURRENT_SOURCE_DIR}/src/include/structures
  ${CMAKE_CURRENT_SOURCE_DIR}/src/include/utils
)

add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDE_DIRS})

find_package(Threads REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE Threads::Threads)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -std=c++23 -fexperimental-library -ftemplate-backtrace-limit=0 -O3")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall --pedantic -g3 -ggdb")

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)