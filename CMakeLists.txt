cmake_minimum_required(VERSION 3.26)
project(cross_platform_bullet_hell_shared LANGUAGES CXX)

file(GLOB_RECURSE SHARED_SRC CONFIGURE_DEPENDS
    library/*.cpp
)

add_library(shared_lib ${SHARED_SRC})

target_include_directories(shared_lib PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_compile_features(shared_lib PUBLIC cxx_std_17)

# Link OS-specific libraries
# Winsock2
if(WIN32)
    if (MINGW)
        target_link_libraries(shared_lib PRIVATE mingw32)
    endif()

    target_link_libraries(shared_lib PRIVATE ws2_32)
endif()