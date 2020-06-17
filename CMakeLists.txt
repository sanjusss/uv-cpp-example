# CMakeList.txt: HelloWorld 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
cmake_minimum_required (VERSION 3.8)

project ("HelloWorld")

add_subdirectory(${PROJECT_SOURCE_DIR}/uv-cpp)

include_directories(${UV_CPP_HEADERS_DIR})


# 将源代码添加到此项目的可执行文件。
add_executable (${PROJECT_NAME} "HelloWorld.cpp" "HelloWorld.h")

target_link_libraries(${PROJECT_NAME} uv_cpp)
# TODO: 如有需要，请添加测试并安装目标。
