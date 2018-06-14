cmake_minimum_required (VERSION 2.8.11)
project(pool)

if (DEFINED ENV{GRAFT_DIR})
    get_filename_component(GRAFT_DIR $ENV{GRAFT_DIR} ABSOLUTE)
    message("Using GraftNetwork source from env ${GRAFT_DIR}")
else()
    get_filename_component(GRAFT_DIR "${CMAKE_SOURCE_DIR}/../GraftNetwork" ABSOLUTE)
    message("GraftNetwork surce directory is not defined, using default ${GRAFT_DIR}")
endif()

add_subdirectory(hashing)
add_subdirectory(cnutil)

add_custom_command(
    OUTPUT build/bin
    COMMAND build/env.sh go get -v ./...
)

add_custom_target(build ALL DEPENDS hashing cnutil ${CMAKE_CURRENT_BINARY_DIR}/build/bin)
