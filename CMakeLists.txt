# CMakeList.txt: HelloWorld 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
cmake_minimum_required (VERSION 2.8)

project ("uv-cpp-examples")

SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11   -O2")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11  -O2")

add_subdirectory(${PROJECT_SOURCE_DIR}/uv-cpp)

include_directories(${UV_CPP_HEADERS_DIR})
include_directories(${PROJECT_SOURCE_DIR}/asio/asio/include)

# 将源代码添加到此项目的可执行文件。
MACRO(SUBDIRLIST result curdir)
  FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)
  SET(dirlist "")
  FOREACH(child ${children})
    IF(IS_DIRECTORY ${curdir}/${child})
      LIST(APPEND dirlist ${child})
    ENDIF()
  ENDFOREACH()
  SET(${result} ${dirlist})
ENDMACRO()

set(EXAMPLES_DIR ${PROJECT_SOURCE_DIR}/uv-cpp/examples)
SUBDIRLIST(EXAMPLES ${EXAMPLES_DIR} )

FOREACH(example ${EXAMPLES})
    set(example_sources "")
    aux_source_directory(${EXAMPLES_DIR}/${example} example_sources)
    add_executable (${example} ${example_sources})
    target_link_libraries(${example} uv_cpp)
ENDFOREACH()


# TODO: 如有需要，请添加测试并安装目标。
