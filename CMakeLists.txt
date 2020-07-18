cmake_minimum_required(VERSION 3.15)

project(CSGeomPP)

set(EXTLIB "${CMAKE_CURRENT_SOURCE_DIR}/third_party")

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT CSGeomPP)
add_executable(CSGeomPP src/main.cpp)


#GLM
set(GLM_DIR "${EXTLIB}/glm")
add_subdirectory(${EXTLIB}/glm)
target_include_directories(${PROJECT_NAME} PRIVATE "${GLM_DIR}")

#GLFW
set(GLFW_DIR "${EXTLIB}/glfw")
set(GLFW_BUILD_EXAMPLES OFF CACHE INTERNAL "Build the GLFW example programs")
set(GLFW_BUILD_TESTS OFF CACHE INTERNAL "Build the GLFW test programs")
set(GLFW_BUILD_DOCS OFF CACHE INTERNAL "Build the GLFW documentation")
set(GLFW_INSTALL OFF CACHE INTERNAL "Generate installation target")
add_subdirectory(${GLFW_DIR})
target_link_libraries(${PROJECT_NAME} "glfw" "${GLFW_LIBRARIES}")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLFW_DIR}/include")
target_compile_definitions(${PROJECT_NAME} PRIVATE "GLFW_INCLUDE_NONE")

#GLAD
set(GLAD_DIR "${EXTLIB}/glad")
add_library(glad "${GLAD_DIR}/src/glad.c")
target_include_directories("glad" PRIVATE "${GLAD_DIR}/include")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLAD_DIR}/include")
target_link_libraries(${PROJECT_NAME} glad "${CMAKE_DL_LIBS}")

