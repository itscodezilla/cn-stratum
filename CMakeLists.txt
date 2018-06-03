cmake_minimum_required (VERSION 2.8.11)
project(pool)

if (DEFINED ENV{STELLITE_DIR})
    get_filename_component(STELLITE_DIR $ENV{STELLITE_DIR} ABSOLUTE)
    message("Using Stellite source from env ${STELLITE_DIR}")
else()
    get_filename_component(STELLITE_DIR "${CMAKE_SOURCE_DIR}/../Stellite" ABSOLUTE)
    message("Stellite source directory is not defined, using default ${STELLITE_DIR}")
endif()

add_subdirectory(hashing)
add_subdirectory(cnutil)

add_custom_command(
    OUTPUT build/bin
    COMMAND build/env.sh go get -v ./...
)

add_custom_target(build ALL DEPENDS hashing cnutil ${CMAKE_CURRENT_BINARY_DIR}/build/bin)
