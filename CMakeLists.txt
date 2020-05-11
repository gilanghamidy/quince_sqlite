cmake_minimum_required(VERSION 3.16)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

project(libquince-sqlite VERSION 0.1)

find_library(SQLITE_LIB sqlite3)
if(NOT SQLITE_LIB)
  message(FATAL_ERROR "sqlite3 library not found")
endif()

find_library(SQLITE_LIB boost)
if(NOT SQLITE_LIB)
  message(FATAL_ERROR "boost library not found")
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_library(quince-sqlite SHARED ${LIBQUINCE_SOURCES})
target_include_directories(quince-sqlite
    PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

if(DEFINED QUINCE_SOURCE_ROOT)
target_include_directories(quince-sqlite
    PUBLIC "${QUINCE_SOURCE_ROOT}/include"
)
endif()

add_subdirectory (src)