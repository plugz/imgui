cmake_minimum_required(VERSION 3.10)
project(imgui_example_gl4 C CXX)

set(GLFW_DIR ../glfw) # Set this to point to an up-to-date GLFW repo
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
add_subdirectory(${GLFW_DIR} binary_dir EXCLUDE_FROM_ALL)

add_executable(example_gl3
        examples/example_glfw_opengl3/main.cpp
        examples/imgui_impl_glfw.cpp
        examples/imgui_impl_opengl3.cpp
        examples/libs/gl3w/GL/gl3w.c
        imgui.cpp
        imgui_draw.cpp
        imgui_demo.cpp
        imgui_widgets.cpp)
target_include_directories(example_gl3 PRIVATE . ${GLFW_DIR}/include examples examples/libs/gl3w)
target_link_libraries(example_gl3 PRIVATE glfw GL dl)
set_target_properties(example_gl3 PROPERTIES
        CXX_STANDARD 17
        CXX_STANDARD_REQUIRED ON
        CXX_EXTENSIONS OFF
        C_STANDARD 11
        C_STANDARD_REQUIRED ON
        C_EXTENSIONS OFF)
