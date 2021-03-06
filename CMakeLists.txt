cmake_minimum_required(VERSION 3.0)

project(dadafilterbank C)

set(CMAKE_C_FLAGS_RELEASE "-O3 -march=native") 

set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)

find_package (psrdada REQUIRED)
find_package (CUDA REQUIRED)

# expose some variables to the source code
set (dadafilterbank_VERSION_MAJOR 0)
set (dadafilterbank_VERSION_MINOR 1)
configure_file ("config.h.in" "${PROJECT_BINARY_DIR}/config.h")
include_directories ("${PROJECT_BINARY_DIR}")

set(HEADERS
        filterbank.h
)

set(SOURCES
    filterbank.c
    main.c
)

add_executable(dadafilterbank ${SOURCES} ${HEADERS})

target_link_libraries(dadafilterbank ${PSRDADA_LIBRARIES} ${CUDA_LIBRARIES})

install(TARGETS dadafilterbank RUNTIME DESTINATION bin)
