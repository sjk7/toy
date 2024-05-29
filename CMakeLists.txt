cmake_minimum_required(VERSION 3.0.0)
project(toy VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()


if (UNIX)
    add_definitions(-DPLATFORM_LINUX)
    message(STATUS "** UNIX (Mac, Linux compile **)")
    find_package(X11 REQUIRED)
    message(STATUS "X11_FOUND = ${X11_FOUND}")
    message(STATUS "X11_INCLUDE_DIR = ${X11_INCLUDE_DIR}")
    message(STATUS "X11_LIBRARIES = ${X11_LIBRARIES}")

    include_directories(${X11_INCLUDE_DIR})
    include_directories(/opt/X11/include/)

    else(
        message(STATUS "** Windows compile **)")
        add_definitions(-DPLATFORM_WIN32)
        )
endif (UNIX)

add_executable(toy main.c)

if (UNIX)
    target_include_directories(toy PRIVATE ${/opt/X11/include/})

    target_link_libraries(${PROJECT_NAME}
        ${X11_LIBRARIES}
    )
endif (UNIX)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
