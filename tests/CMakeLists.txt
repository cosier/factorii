cmake_minimum_required(VERSION 3.6)
project(app-tests)

# This project uses C11 Standard
set( CMAKE_C_STANDARD 11 )

# Treat all warnings as intense errors.
if(NOT MSVC)
set( CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Werror")
endif()

file(GLOB_RECURSE HELPER_LIB helpers/*.c helpers/*.h)

# message ( FATAL_ERROR "HELPER_SRC: ${HELPER_LIB}" )
include_directories(
  "${CMAKE_SOURCE_DIR}/tests"
  "${CMAKE_SOURCE_DIR}/src"
  )

add_library(tests STATIC ${HELPER_LIB})
# Test Executable that utilises the library.

add_executable(test-main test_main.c)

# Alias a shorter name, shortcut.
set(lib ${APP_LIB_NAME})

# Link up main executable with our Library: libdimappio
target_link_libraries( test-main ${lib} tests)

# Enable CTests suite reporting

add_test(NAME test-main COMMAND test-main)

