﻿cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("3Dprog24")

include_directories(includes)
include_directories(includes/imgui)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/core)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/Games/TestGame)

#Add IMGUI headers
set( IMGUI_HEADERS
    includes/imgui/imgui.h
    includes/imgui/imconfig.h
    includes/imgui/imgui_impl_opengl3.h
    includes/imgui/imgui_impl_glfw.h
    includes/imgui/imgui_impl_opengl3_loader.h
)

#Add IMGUI sources
set( IMGUI_SOURCE
    includes/imgui/imgui.cpp
    includes/imgui/imgui_demo.cpp
    includes/imgui/imgui_draw.cpp
    includes/imgui/imgui_widgets.cpp
    includes/imgui/imgui_impl_opengl3.cpp
    includes/imgui/imgui_impl_glfw.cpp
    includes/imgui/imgui_tables.cpp
)

set (HEADER_FILES
  includes/stb_image.h
  core/Shader.h
  core/Camera.h
  core/Window.h
  core/Application.h
  core/Material.h
  core/Mesh.h
  core/Renderer.h
  core/Scene.h
  core/Texture.h
  core/Scene.h
  core/Actor.h
  core/Logger.h
  core/Types.h  
  core/Transform.h
  core/Tag.h
  core/Vertex.h
  core/SceneGraph.h
  core/Controller.h 
  core/Defines.h 
  core/CameraController.h 
  )

set (SRC_FILES
  3Dprog24.cpp
  includes/glad.c
  core/Shader.cpp
  core/Camera.cpp
  core/Window.cpp
  core/Application.cpp
  core/Texture.cpp 
  core/Material.cpp     
  core/Mesh.cpp
  core/Scene.cpp
  core/Actor.cpp
  core/CameraController.cpp
)

add_subdirectory(libs/glfw-3.3.9)

# Add source to this project's executable.
add_executable(3Dprog24 ${IMGUI_HEADERS} ${IMGUI_SOURCE} ${HEADER_FILES} ${SRC_FILES})

#target_link_libraries(3Dprog24 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/libs/glfw3.lib)
target_link_libraries(3Dprog24 glfw)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET 3Dprog24 PROPERTY CXX_STANDARD 20)
endif()