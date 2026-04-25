include_directories(${SunsetEngine_SOURCE_DIR}/Engine/include)
# I assume you want to use LibProject as a library in MainProject.
add_executable(Sunset SunsetEngine.cpp)

