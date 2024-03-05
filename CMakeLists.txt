cmake_minimum_required(VERSION 3.0.0)
project(opengl-practice VERSION 0.1.0)

include(CTest)
enable_testing()

add_executable(opengl-practice
    main.cpp
    Window.h
    Window.cpp
    Shader.h
    Shader.cpp
    Mesh.h
    Mesh.cpp
    Camera.h
    Camera.cpp
    Texture.h
    Texture.cpp
    Light.h
    Light.cpp
    Material.h
    Material.cpp
    DirectionalLight.h
    DirectionalLight.cpp
    PointLight.h
    PointLight.cpp
    SpotLight.h
    SpotLight.cpp
    Model.h
    Model.cpp
    CommonValues.h
)

# glfw
find_package(glfw3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

# glew
add_definitions(-DGLEW_STATIC)
add_subdirectory(external/glew EXCLUDE_FROM_ALL)
target_link_libraries(${PROJECT_NAME} PRIVATE libglew_static)

# glm
add_subdirectory(external/glm EXCLUDE_FROM_ALL)
target_link_libraries(${PROJECT_NAME} PRIVATE glm)

# assimp
add_subdirectory(external/assimp EXCLUDE_FROM_ALL)
target_link_libraries(${PROJECT_NAME} PRIVATE assimp)

# stb
include_directories(external/stb)

add_custom_command(
        TARGET ${PROJECT_NAME} PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E create_symlink
                ${CMAKE_SOURCE_DIR}/Shaders
                ${CMAKE_CURRENT_BINARY_DIR}/Shaders)

add_custom_command(
        TARGET ${PROJECT_NAME} PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E create_symlink
                ${CMAKE_SOURCE_DIR}/Textures
                ${CMAKE_CURRENT_BINARY_DIR}/Textures)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

include(CPack)