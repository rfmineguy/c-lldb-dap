cmake_minimum_required(VERSION 3.20)
project(c-imgui-test LANGUAGES C CXX)

include(FetchContent)
FetchContent_Declare(cimgui GIT_REPOSITORY https://github.com/cimgui/cimgui.git GIT_TAG docking_inter GIT_SHALLOW)
FetchContent_MakeAvailable(cimgui)

set(GLFW_VERSION 3.4)
include(FetchContent)
FetchContent_Declare(glfw GIT_REPOSITORY https://github.com/glfw/glfw.git GIT_TAG 3.5.1)
FetchContent_MakeAvailable(glfw)

message(STATUS "cimgui-src :: ${cimgui_SOURCE_DIR}")
message(STATUS "glfw-src :: ${glfw_SOURCE_DIR}")
set(IMGUI_BACKEND ${cimgui_SOURCE_DIR}/imgui/backends/imgui_impl_glfw.cpp ${cimgui_SOURCE_DIR}/imgui/backends/imgui_impl_opengl3.cpp)
add_executable(c-imgui-test src/main.c ${IMGUI_BACKEND})
target_include_directories(c-imgui-test PRIVATE ${cimgui_SOURCE_DIR} ${glfw_SOURCE_DIR})
target_link_libraries(c-imgui-test PRIVATE cimgui glfw GL)
