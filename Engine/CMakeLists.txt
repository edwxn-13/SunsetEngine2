set(CMAKE_CXX_STANDARD 23)
project(Engine)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
#set(ASSIMP_BUILD_ZLIB ON)
set(ASSIMP_BUILD_ASSIMP_TOOLS ON)
#set(ASSIMP_HUNTER_ENABLED ON)
add_subdirectory(external/glfw)
add_subdirectory(external/assimp)

add_library(glad STATIC external/glad/src/glad.c)
target_include_directories(glad PUBLIC external/glad/include/)

file(COPY ${CMAKE_SOURCE_DIR}/Engine/Shaders DESTINATION ${CMAKE_BINARY_DIR})

set(PROJECT_SOURCES
    src/Assets/MeshObject/MeshObject.cpp
    src/Assets/MeshObject/SMeshObject.cpp
    src/Assets/Scenes/MainScene.cpp
    src/Assets/Ship/ShipController/ShipController.cpp
    src/Camera/camera.cpp
    src/Components/CameraComponent/CameraComponent.cpp
    src/Components/Component.cpp
    src/Components/LightComponent/LightComponent.cpp
    src/Components/MeshComponent/MeshComponent.cpp
    src/Components/MeshRenderer/MeshRenderer.cpp
    src/Components/PlanetRenderer/PlanetNode/PlanetNode.cpp
    src/Components/PlanetRenderer/PlanetRenderer.cpp
    src/Components/PlanetRenderer/PlanetSettings/PlanetSettings.cpp
    src/Components/PrimativeRenderer/PrimativeRenderer.cpp
    src/Components/RenderingComponent.cpp
    src/Components/Rigidbody/CollisionComponent/CollisionComponent.cpp
    src/Components/Rigidbody/Rigidbody.cpp
    src/Engine/Engine.cpp
    src/Engine/EngineUtils.cpp
    src/Engine/Renderer/Material/Material.cpp
    src/Engine/Renderer/Renderer.cpp
    src/Engine/Renderer/ShaderManager/ShaderManager.cpp
    src/Engine/Renderer/Shadows/shadow.cpp
    src/Engine/Scene/Scene.cpp
    src/Engine/SceneManager/SceneManager.cpp
    src/Engine/Utility/Time.cpp
    src/EngineObjects/EngineObject.cpp
    src/EngineObjects/Planet/Planet.cpp
    src/EngineObjects/PrimativeObject/PrimativeObject.cpp
    src/EngineObjects/Skybox/Skybox.cpp
    src/EngineObjects/Sun/Sun.cpp
    src/Maths/MathHeader.cpp
    src/Maths/SimplexNoise.cpp
    src/Maths/Vector3d.cpp
    src/Physics/Collider/BoxCollider/BoxCollider.cpp
    src/Physics/Collider/ColliderManager.cpp
    src/Physics/Collider/Ray/Ray.cpp
    src/Physics/Collider/SphereCollider/SphereCollider.cpp
    src/Physics/ColliderMath.cpp
    src/Physics/CollisionGrid/CollisionGrid.cpp
    src/SunsetEngine.cpp
    src/Utils/file.cpp
    src/Utils/ModelParser/ModelParser.cpp
    src/Utils/obj.cpp
    src/Utils/shader.cpp
    src/Utils/texture.cpp
)

set(PROJECT_HEADERS
    src/Assets/MeshObject/MeshObject.h
    src/Assets/MeshObject/SMeshObject.h
    src/Assets/Scenes/MainScene.h
    src/Assets/Ship/ShipController/ShipController.h
    src/Camera/camera.h
    src/Components/CameraComponent/CameraComponent.h
    src/Components/Component.h
    src/Components/LightComponent/LightComponent.h
    src/Components/MeshComponent/MeshComponent.h
    src/Components/MeshRenderer/MeshRenderer.h
    src/Components/PlanetRenderer/PlanetMath.h
    src/Components/PlanetRenderer/PlanetMath.inl
    src/Components/PlanetRenderer/PlanetNode/PlanetNode.h
    src/Components/PlanetRenderer/PlanetRenderer.h
    src/Components/PlanetRenderer/PlanetSettings/PlanetSettings.h
    src/Components/PrimativeRenderer/PrimativeRenderer.h
    src/Components/RenderingComponent.h
    src/Components/Rigidbody/CollisionComponent/CollisionComponent.h
    src/Components/Rigidbody/Rigidbody.h
    src/Engine/Engine.h
    src/Engine/EngineUtils.h
    src/Engine/Renderer/Material/Material.h
    src/Engine/Renderer/Renderer.h
    src/Engine/Renderer/ShaderManager/ShaderManager.h
    src/Engine/Renderer/Shadows/shadow.h
    src/Engine/Scene/Scene.h
    src/Engine/SceneManager/SceneManager.h
    src/Engine/Utility/Time.h
    src/EngineObjects/EngineObject.h
    src/EngineObjects/EngineObject.inl
    src/EngineObjects/Planet/Planet.h
    src/EngineObjects/PrimativeObject/PrimativeObject.h
  )

  add_executable(${PROJECT_NAME}
  ${PROJECT_HEADERS}
  ${PROJECT_SOURCES}
)

target_include_directories(${PROJECT_NAME} PRIVATE
  ${CMAKE_SOURCE_DIR}/Engine/src
)

find_package(glm CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE glm::glm)
target_link_libraries(${PROJECT_NAME} PRIVATE
    glm
    glfw
    glad
    assimp
)

