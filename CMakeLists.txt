cmake_minimum_required(VERSION 3.9)
cmake_policy(SET CMP0072 NEW)
project(GP)

# set(OpenGL_GL_PREFERENCE GLVND)
find_package(glfw3 3.2 REQUIRED)
include(FindOpenGL)


if(MSVC)
  set(CMAKE_CXX_FLAGS "/std:c++latest /W4 /WX /MP /EHsc /DNOMINMAX /DBOOST_SCOPE_EXIT_CONFIG_USE_LAMBDAS=1 /D_HAS_AUTO_PTR_ETC=1")
  set(CMAKE_CXX_FLAGS_DEBUG "/MTd /Zi")
  set(CMAKE_CXX_FLAGS_RELEASE "/MT /DNDEBUG")

  add_definitions(-DUNICODE)
  add_definitions(-D_UNICODE)
  add_definitions(-D_SCL_SECURE_NO_WARNINGS)
else()
  set(CMAKE_CXX_FLAGS "-std=c++1y -Wall -Wextra -pedantic-errors")
  set(CMAKE_CXX_FLAGS_DEBUG "-g -O0") # -fno-inline -pg
  set(CMAKE_CXX_FLAGS_RELEASE "-O2 -DNDEBUG")
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/lib")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")


add_executable(gp src/main.cpp)
target_link_libraries(gp ${OPENGL_LIBRARIES} glfw)
