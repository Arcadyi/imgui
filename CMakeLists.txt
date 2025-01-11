project(imgui C CXX ASM)

find_package(SDL3 REQUIRED)
find_package(Vulkan REQUIRED)

set(COMPILE_WGPU OFF)

if (APPLE)
    enable_language(SWIFT)
    enable_language(OBJCXX)
    set(IMGUI_FILES
            ${IMGUI_FILES}
            backends/imgui_impl_osx.h
            backends/imgui_impl_osx.mm)
ELSEIF(WIN32)
    set(IMGUI_FILES
            ${IMGUI_FILES}
            backends/imgui_impl_dx10.cpp
            backends/imgui_impl_dx10.h
            backends/imgui_impl_dx11.cpp
            backends/imgui_impl_dx11.h
            backends/imgui_impl_dx12.cpp
            backends/imgui_impl_dx12.h
            backends/imgui_impl_win32.cpp
            backends/imgui_impl_win32.h)
ELSEIF(UNIX)
    set(IMGUI_FILES
            ${IMGUI_FILES})
ENDIF()

IF(COMPILE_WGPU)
    set(IMGUI_FILES
            ${IMGUI_FILES}
            backends/imgui_impl_wgpu.cpp
            backends/imgui_impl.wgpu.h)
ENDIF()

set(IMGUI_FILES
        ${IMGUI_FILES}
        imconfig.h
        imgui.cpp
        imgui.h
        imgui_demo.cpp
        imgui_draw.cpp
        imgui_internal.h
        imgui_tables.cpp
        imgui_widgets.cpp
        imstb_rectpack.h
        imstb_textedit.h
        imstb_truetype.h
        backends/imgui_impl_opengl2.cpp
        backends/imgui_impl_opengl2.h
        backends/imgui_impl_opengl3.cpp
        backends/imgui_impl_opengl3.h
        backends/imgui_impl_opengl3_loader.h
        backends/imgui_impl_sdl3.cpp
        backends/imgui_impl_sdl3.h
        backends/imgui_impl_sdlrenderer3.cpp
        backends/imgui_impl_sdlrenderer3.h
        backends/imgui_impl_vulkan.cpp
        backends/imgui_impl_vulkan.h)

include_directories(imgui ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/backends)
add_library(imgui STATIC ${IMGUI_FILES})
target_link_libraries(imgui PRIVATE Vulkan::Vulkan SDL3::SDL3)