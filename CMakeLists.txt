cmake_minimum_required(VERSION 3.16)
project(luajit-decompiler-v2 CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE Release)
endif()

add_executable(luajit-decompiler-v2
  main.cpp
  ast/ast.cpp
  bytecode/bytecode.cpp
  bytecode/prototype.cpp
  lua/lua.cpp)

if(MSVC)
  target_compile_options(luajit-decompiler-v2 PRIVATE /J)
else()
  target_compile_options(luajit-decompiler-v2 PRIVATE -funsigned-char)
  find_package(Threads REQUIRED)
  target_link_libraries(luajit-decompiler-v2 PRIVATE Threads::Threads)
endif()
