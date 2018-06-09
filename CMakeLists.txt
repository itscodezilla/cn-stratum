cmake_minimum_required (VERSION 2.8.11)
project(pool)

if (DEFINED ENV{MASARI_DIR})
    get_filename_component(MASARI_DIR $ENV{MASARI_DIR} ABSOLUTE)
    message("Using Masari source from env ${MASARI_DIR}")
else()
    get_filename_component(MASARI_DIR "${CMAKE_SOURCE_DIR}/../masari" ABSOLUTE)
    message("Masari surce directory is not defined, using default ${MASARI_DIR}")
endif()

add_subdirectory(hashing)
add_subdirectory(cnutil)

add_custom_command(
    OUTPUT build/bin
    COMMAND build/env.sh go get -v ./...
)

add_custom_target(build ALL DEPENDS hashing cnutil ${CMAKE_CURRENT_BINARY_DIR}/build/bin)
