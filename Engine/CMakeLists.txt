project(SunsetEngine)

file(GLOB_RECURSE ENGINE_SOURCES
  src/*.cpp
)
add_library(${PROJECT_NAME} STATIC ${ENGINE_SOURCES})
add_library(sub::lib1 ALIAS ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_SOURCE_DIR}/lib)
target_link_libraries(${PROJECT_NAME} PUBLIC glfw)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_SOURCE_DIR}/include)


