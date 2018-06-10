set(LIB "hashing")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11 -D_GNU_SOURCE")

include_directories("${MUTEX_DIR}/contrib/epee/include")
include_directories("${MUTEX_DIR}/src")

link_directories(${MUTEX_DIR}/src/crypto)

add_library(${LIB} SHARED src/hashing.c)

target_link_libraries(${LIB} cncrypto)
