cmake_minimum_required(VERSION 3.14)

# Project name
project(wxSQLite3Library LANGUAGES C CXX)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Enable FetchContent for wxWidgets
include(FetchContent)

message(STATUS "Fetching wxWidgets...")
FetchContent_Declare(
  wxWidgets
  GIT_REPOSITORY https://github.com/wxWidgets/wxWidgets.git
  GIT_TAG master
)

FetchContent_MakeAvailable(wxWidgets)
message(STATUS "wxWidgets has been fetched.")

# Add include directories
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# Source files
set(SOURCES
    src/wxsqlite3.cpp
    src/sqlite3mc_amalgamation.c
)

# Add the static library target
add_library(wxSQLite3 STATIC ${SOURCES})

# Link wxWidgets to the library
target_link_libraries(wxSQLite3 PRIVATE wxcore wxbase)

# Define include directories for the library
target_include_directories(wxSQLite3 PRIVATE include)

# Optional: Add version info
set_target_properties(wxSQLite3 PROPERTIES VERSION 1.0.0 SOVERSION 1)

# Installation instructions (optional)
install(TARGETS wxSQLite3 DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)
