cmake_minimum_required(VERSION 3.6)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED on)

project(imgui)

option(BUILD_DEMO ON)

set(IMGUI_HEADERS
    imconfig.h
    imgui_internal.h
    imgui_user.h
    imgui_user.inl
    imgui.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h)

set(IMGUI_ADDON_HEADERS
    addons/imgui_user.h
    addons/imgui_user.inl)

set(IMGUI_SOURCES
    imgui_draw.cpp
    imgui.cpp)

add_library(imgui ${IMGUI_SOURCES} ${IMGUI_HEADERS})
target_compile_definitions(imgui PUBLIC
    IMGUI_INCLUDE_IMGUI_USER_H)
target_include_directories(imgui PUBLIC .)

install(FILES ${IMGUI_HEADERS} ${IMGUI_ADDON_HEADERS} DESTINATION include/imgui)
install(DIRECTORY addons DESTINATION include/imgui
    FILES_MATCHING PATTERN "*.h")
install(TARGETS imgui DESTINATION lib)

# if (BUILD_DEMO)
#     set(IMGUI_DEMO_FILES
#         imgui_demo.cpp)

#     set(IMGUI_IMPL_GLFW_FILES
#         examples/imgui_impl_glfw.cpp
#         examples/imgui_impl_glfw.h)

#     add_executable(imgui_demo
#         ${IMGUI_DEMO_FILES}
#         ${IMGUI_IMPL_GLFW_FILES}
#         imgui_demo.cpp
#         examples/addons_examples/main.cpp)

#     add_dependencies(imgui_demo imgui)
#     target_include_directories(imgui_demo PUBLIC
#         .
#         /usr/local/include)
#     target_compile_definitions(imgui_demo PUBLIC 
#         IMGUI_USE_GLFW_BINDING)
#     target_link_libraries(imgui_demo
#         imgui
#         -L/usr/local/lib
#         glfw3 sqlite3
#         "-framework OpenGL")
# endif()
