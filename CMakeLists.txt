cmake_minimum_required(VERSION 3.5)
project(partial)

find_package(BISON 3.0.4)
find_package(FLEX 2.6.0)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

BISON_TARGET(y.tab.o calculator_partial.y ${CMAKE_CURRENT_BINARY_DIR}/y.tab.c COMPILE_FLAGS -vd)
FLEX_TARGET(lex.yy.o calculator_partial.l  ${CMAKE_CURRENT_BINARY_DIR}/lex.yy.c)
ADD_FLEX_BISON_DEPENDENCY(lex.yy.o y.tab.o)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_executable(calculator_partial
  ${BISON_y.tab.o_OUTPUTS}
  ${FLEX_lex.yy.o_OUTPUTS}
  calculator_interpreter_partial.c
)
