# Particles

cmake_minimum_required(VERSION 3.10)
project(Particles VERSION 1.1)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if (MSVC)
    add_compile_options(/W3 /D_CRT_SECURE_NO_WARNINGS )
else()
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()

#"-DCMAKE_TOOLCHAIN_FILE=C:/bin/vcpkg/scripts/buildsystems/vcpkg.cmake"

message( CHECK_START "[test] CMake message ${PROJECT_BINARY_DIR} ...")
message( CHECK_START "[test] Generator is ${CMAKE_GENERATOR}")
message( CHECK_START "[test] Prefix is ${CMAKE_PREFIX_PATH}")

set(CMAKE_INSTALL_PREFIX "${PROJECT_BINARY_DIR}/install" )


find_package(SDL2 CONFIG REQUIRED)
add_executable(part "SDL75-Motion.cpp" "Particle.cpp" "Particle.h" "Screen.cpp" "Screen.h" "Swarm.cpp" "Swarm.h" )

install( TARGETS part DESTINATION bin )

target_link_libraries(part PRIVATE SDL2::SDL2 SDL2::SDL2main)
enable_testing()

add_test( NAME Runs COMMAND part 1000 1024 768 )

#fim
