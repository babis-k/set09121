cmake_minimum_required(VERSION 3.9)
# Compiler flags
if (MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP /EHsc" CACHE INTERNAL "" FORCE)
endif()
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(Games_Engineering)

#### setup Directories ####
#Main output directory
set(OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/")
# Ouput all DLLs from all libs into main build folder
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY})

add_custom_target(copy_resources ALL COMMAND ${CMAKE_COMMAND} 
  -E copy_directory
    "${PROJECT_SOURCE_DIR}/res"
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/$<CONFIGURATION>/res
)

set (SMFL_COMPONENTS graphics audio window system)
set (SFML_LIBRARIES "")
foreach(x ${SMFL_COMPONENTS})
    list (APPEND SFML_LIBRARIES debug sfml-${x}_d optimized sfml-${x})
endforeach()
set( SFML_LIBRARY_DIR ${PROJECT_SOURCE_DIR}/contrib/sfml/lib/${ConfigurationName})
set( SFML_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/contrib/sfml/include)

set( BOX2D_LIBRARIES box2d)
set( BOX2D_LIBRARY_DIR ${PROJECT_SOURCE_DIR}/contrib/box2d/lib/${ConfigurationName})
set( BOX2D_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/contrib/box2d/include)

link_directories(${SFML_LIBRARY_DIR} ${BOX2D_LIBRARY_DIR})

add_subdirectory(lib)
add_subdirectory(samples)