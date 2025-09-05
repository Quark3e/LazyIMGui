cmake_minimum_required(VERSION 3.18)

set(CMAKE_TOOLCHAIN_FILE "C:/Users/berkh/Libraries/vcpkg/scripts/buildsystems/vcpkg.cmake")
project(lazyimgui)

set(CMAKE_CXX_STANDARD 17)

find_package(imgui CONFIG REQUIRED)


set(DIR__INCLUDES   "${PROJECT_SOURCE_DIR}/include")
set(DIR__SOURCES    "${PROJECT_SOURCE_DIR}/src")
set(DIR__LIBRARIES  "${PROJECT_SOURCE_DIR}/lib")


add_library(lazyimgui STATIC ${DIR__INCLUDES}/lazyimgui.hpp ${DIR__SOURCES}/lazyimgui.cpp)
add_library(lazyimgui::lazyimgui ALIAS lazyimgui )


target_include_directories(lazyimgui PUBLIC ${DIR__INCLUDES})
target_include_directories(lazyimgui PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>)



include(GNUInstallDirs)

install(TARGETS lazyimgui
        EXPORT lazyimgui_targets
        INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")

export( EXPORT lazyimgui_targets
        NAMESPACE lazyimgui::
        FILE "${CMAKE_INSTALL_LIBDIR}/cmake/lazyimgui/lazyimgui-config.cmake")




