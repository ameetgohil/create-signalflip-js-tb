cmake_minimum_required(VERSION 3.10)
project (dut)
#include_directories($CMAKE_JS_INC})
set(VERPATH "/usr/local/share/verilator")
if(DEFINED ENV{VERILATOR_ROOT})
  set(VERPATH ENV{VERILATOR_ROOT})
endif()
file(GLOB SOURCE_FILES "cppsrc/*.cpp")
file(GLOB VERLIBS "obj_dir/*.a")
add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})
link_directories(${CMAKE_SOURCE_DIR}/obj_dir)
target_include_directories(${PROJECT_NAME}
  PRIVATE ${CMAKE_SOURCE_DIR}/node_modules/node-addon-api
  PRIVATE ${VERPATH}/include
  PRIVATE ${VERPATH}/include/vltstd
  PRIVATE ${VERPATH}/include/gtkwave
  PRIVATE ./obj_dir
  PRIVATE ${CMAKE_JS_INC})
set_target_properties(${PROJECT_NAME} PROPERTIES PREFIX "" SUFFIX ".node")
target_link_libraries(${PROJECT_NAME} ${CMAKE_JS_LIB} ${VERLIBS})

