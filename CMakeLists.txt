# CMakeList.txt : CMake project for WeatherStationServer, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.12)

project ("WeatherStationServer")

message("Project name is: ${PROJECT_NAME}")

# Add source to this project's executable.
set(CMAKE_CXX_STANDARD 20)

find_package(SOCI REQUIRED)

# Add source files
file(GLOB_RECURSE SOURCES "src/*.cpp" "src/*.h")

# Group source files by directory
foreach(file ${SOURCES}) 
    get_filename_component(path ${file} PATH)
    string(REPLACE "${CMAKE_CURRENT_SOURCE_DIR}/src/" "" group ${path})
    string(REPLACE "/" "\\" group ${group})
    source_group("src\\${group}" FILES ${file})
endforeach()

# Add executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link SOCI library to executable
target_link_libraries(${PROJECT_NAME} SOCI::core SOCI::odbc)