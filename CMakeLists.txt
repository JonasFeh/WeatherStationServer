cmake_minimum_required(VERSION 3.14)

project(WeatherStationServer)

# Add source files
file(GLOB_RECURSE SOURCES "src/*.cpp" "src/*.h")

# Group source files by directory
foreach(file ${SOURCES}) 
    get_filename_component(path ${file} PATH)
    string(REPLACE "${CMAKE_CURRENT_SOURCE_DIR}/src/" "" group ${path})
    string(REPLACE "/" "\\" group ${group})
    source_group("src\\${group}" FILES ${file})
endforeach()

# Create an executable target for your project
add_executable(WeatherStationServer ${SOURCES})

# Add POCO
add_subdirectory(Poco)

# Target headers
target_include_directories(${PROJECT_NAME} 
    PUBLIC Poco/include)

# Target libraries
target_link_directories(${PROJECT_NAME} 
    PRIVATE Poco/src)

# Link licraries
target_link_libraries(${PROJECT_NAME} Poco)
