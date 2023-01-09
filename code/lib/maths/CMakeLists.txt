project(maths)
file(GLOB_RECURSE SOURCE_FILES *.cpp *.h)
add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})
target_include_directories(${PROJECT_NAME} PUBLIC . ${SFML_INCLUDE_DIR})