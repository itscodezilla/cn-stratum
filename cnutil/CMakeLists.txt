set(CXXLIB "cnutil")

find_package(Boost COMPONENTS thread system program_options date_time filesystem REQUIRED)

# Flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -D_GNU_SOURCE")

include_directories(${Boost_INCLUDE_DIRS})
include_directories("${GRAFT_DIR}/contrib/epee/include")
include_directories("${GRAFT_DIR}/src")
include_directories("${GRAFT_DIR}/external/easylogging++")

link_directories(
    ${GRAFT_DIR}/src/cryptonote_core
    ${GRAFT_DIR}/src/cryptonote_basic
    ${GRAFT_DIR}/src/crypto
    ${GRAFT_DIR}/src/common
    ${GRAFT_DIR}/src/ringct
    ${GRAFT_DIR}/src/blockchain_db
    ${GRAFT_DIR}/external/easylogging++
    ${GRAFT_DIR}/contrib/epee/src
)

# Build library
add_library(${CXXLIB} SHARED src/cnutil.cpp)

target_link_libraries(${CXXLIB}
    cryptonote_core
    cryptonote_basic
    cncrypto
    common
    ringct
    blockchain_db
    easylogging
    epee
)

target_link_libraries(${CXXLIB}
    ${Boost_THREAD_LIBRARY}
    ${Boost_SYSTEM_LIBRARY}
    ${Boost_PROGRAM_OPTIONS_LIBRARY}
    ${Boost_DATE_TIME_LIBRARY}
    ${Boost_FILESYSTEM_LIBRARY}
)
