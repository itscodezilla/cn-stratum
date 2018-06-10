cmake_minimum_required (VERSION 2.8.11)
project(pool)

if (DEFINED ENV{FONERO_DIR})
    get_filename_component(FONERO_DIR $ENV{FONERO_DIR} ABSOLUTE)
    message("Using Fonero source from env ${FONERO_DIR}")
else()
    get_filename_component(FONERO_DIR "${CMAKE_SOURCE_DIR}/../fonero" ABSOLUTE)
    message("Fonero surce directory is not defined, using default ${FONERO_DIR}")
endif()

add_subdirectory(hashing)
add_subdirectory(cnutil)

add_custom_command(
    OUTPUT build/bin
    COMMAND build/env.sh go get -v ./...
)

add_custom_target(build ALL DEPENDS hashing cnutil ${CMAKE_CURRENT_BINARY_DIR}/build/bin)
