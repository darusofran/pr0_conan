cmake_minimum_required(VERSION 3.25)
project(pr0_conan)

set(CMAKE_CXX_STANDARD 14)

include_directories(.)

add_executable(${pr0_conan}
        igvInterfaz.cpp
        igvInterfaz.h
        pr1.cpp
        igvInterfaz.cpp)

if (LINUX)
    find_path(OPENGL_REGISTRY_INCLUDE_DIRS "GL/glcorearb.h")
    target_include_directories(${pr0_conan} PRIVATE ${OPENGL_REGISTRY_INCLUDE_DIRS})

    find_package(OpenGL REQUIRED)
    target_link_libraries(${pr0_conan} PRIVATE ${OPENGL_LIBRARIES})
    target_include_directories(${pr0_conan} PRIVATE ${OPENGL_INCLUDE_DIR})

    find_package(GLUT REQUIRED)
    target_link_libraries(${pr0_conan} PRIVATE GLUT::GLUT)
endif ()

if (WIN32)
    find_package(opengl_system)
    target_link_libraries(${pr0_conan} opengl::opengl)

    find_package(opengl-registry)
    target_link_libraries(${pr0_conan} opengl-registry::opengl-registry)

    find_package(FreeGLUT)
    target_link_libraries(${pr0_conan} FreeGLUT::freeglut_static)
endif ()
