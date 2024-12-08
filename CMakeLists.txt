project(imgui)

find_library(SDL3 ../SDL)
set(IMGUI_FILES
        imconfig.h
        imgui.h
        imgui_internal.h
        imstb_rectpack.h
        imstb_textedit.h
        imstb_truetype.h
        imgui.cpp
        imgui_demo.cpp
        imgui_draw.cpp
        imgui_tables.cpp
        imgui_widgets.cpp
        backends/imgui_impl_dx10.cpp
        backends/imgui_impl_dx10.h
        backends/imgui_impl_dx11.cpp
        backends/imgui_impl_dx11.h
        backends/imgui_impl_dx12.cpp
        backends/imgui_impl_dx12.h
        backends/imgui_impl_opengl2.cpp
        backends/imgui_impl_opengl2.h
        backends/imgui_impl_opengl3.cpp
        backends/imgui_impl_opengl3.h
        backends/imgui_impl_opengl3_loader.h
        backends/imgui_impl_sdl3.cpp
        backends/imgui_impl_sdl3.h
        backends/imgui_impl_sdlrenderer3.cpp
        backends/imgui_impl_sdlrenderer3.h
        backends/imgui_impl_win32.cpp
        backends/imgui_impl_win32.h
)
include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/backends ../SDL/include)
add_library(imgui STATIC ${IMGUI_FILES})
target_link_libraries(imgui PRIVATE SDL3::SDL3)