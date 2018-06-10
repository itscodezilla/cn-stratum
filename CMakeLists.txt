cmake_minimum_required (VERSION 2.8.11)
project(pool)

if (DEFINED ENV{MUTEX_DIR})
    get_filename_component(MUTEX_DIR $ENV{MUTEX_DIR} ABSOLUTE)
    message("Using Mutex source from env ${MUTEX_DIR}")
else()
    get_filename_component(MUTEX_DIR "${CMAKE_SOURCE_DIR}/../mutex" ABSOLUTE)
    message("Mutex surce directory is not defined, using default ${MUTEX_DIR}")
endif()

add_subdirectory(hashing)
add_subdirectory(cnutil)

add_custom_command(
    OUTPUT build/bin
    COMMAND build/env.sh go get -v ./...
)

add_custom_target(build ALL DEPENDS hashing cnutil ${CMAKE_CURRENT_BINARY_DIR}/build/bin)
