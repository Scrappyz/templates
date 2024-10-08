cmake_minimum_required(VERSION 3.14)

# Declare unit testing framework
FetchContent_Declare(
    GTest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG v1.15.2
)

# Make the framework available for the project
FetchContent_MakeAvailable(GTest)

# Enable unit testing and include the framework
enable_testing()
include(GoogleTest)

# Set unit testing binary output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/bin)

# Add the unit testing target executable
file(GLOB Sources ${CMAKE_CURRENT_SOURCE_DIR}/../src/*.cpp ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)
list(REMOVE_ITEM Sources ${CMAKE_CURRENT_SOURCE_DIR}/../src/main.cpp)
add_executable(!project!_test ${Sources})
target_include_directories(!project!_test PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_libraries(!project!_test PUBLIC gtest_main)

# Add tests
add_test(
    NAME !project!Test
    COMMAND !project!_test
)