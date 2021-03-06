cmake_minimum_required(VERSION 2.8.12)
project(zeda)

add_definitions("-Wall -g -O3")

include_directories(include)

# Build
add_library(zeda_misc src/zeda_misc.c)
add_library(zeda_string src/zeda_string.c)
add_library(zeda_bit src/zeda_bit.c)
add_library(zeda_rand src/zeda_rand.c)
add_library(zeda_array src/zeda_array.c)
add_library(zeda_index src/zeda_index.c)
add_library(zeda_stream src/zeda_stream.c)
add_library(zeda_list src/zeda_list.c)
add_library(zeda_rrtab src/zeda_rrtab.c)
add_library(zeda_strlist src/zeda_strlist.c)
add_library(zeda_option src/zeda_option.c)
add_library(zeda_bfile src/zeda_bfile.c)

add_library(${PROJECT_NAME} SHARED 
    src/zeda_misc.c
    src/zeda_string.c
    src/zeda_bit.c
    src/zeda_rand.c
    src/zeda_array.c
    src/zeda_index.c
    src/zeda_stream.c
    src/zeda_list.c
    src/zeda_rrtab.c
    src/zeda_strlist.c
    src/zeda_option.c
    src/zeda_bfile.c)

# Install
INSTALL (
    DIRECTORY ${CMAKE_SOURCE_DIR}/include/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h*")

install(TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib)

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}-export
    LIBRARY        DESTINATION lib
    INCLUDES       DESTINATION include
    PUBLIC_HEADER  DESTINATION include/${PROJECT_NAME})

install(EXPORT ${PROJECT_NAME}-export
    FILE ${PROJECT_NAME}-config.cmake
    DESTINATION share/cmake/${PROJECT_NAME}
    EXPORT_LINK_INTERFACE_LIBRARIES)