cmake_minimum_required(VERSION 3.4 FATAL_ERROR)

project(vulkan)

set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

add_executable(vulkan-triangle
	main.c)

target_link_libraries(vulkan-triangle
	/usr/lib/libvulkan.so
	/usr/lib/libglfw.so)

add_custom_target(vert.spv
	COMMAND glslangValidator --quiet -V ${CMAKE_SOURCE_DIR}/shader.vert -o ${CMAKE_BINARY_DIR}/vert.spv)

add_custom_target(frag.spv
	COMMAND glslangValidator --quiet -V ${CMAKE_SOURCE_DIR}/shader.frag -o ${CMAKE_BINARY_DIR}/frag.spv)

add_dependencies(vulkan-triangle
    vert.spv
    frag.spv)