cmake_minimum_required(VERSION 3.20)
project(KELBON_TEMPLATE_PROJECT_NAME)

include(cmake/deps.cmake)

file(GLOB_RECURSE KELBON_TEMPLATE_PROJECT_NAME_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

add_library(KELBON_TEMPLATE_PROJECT_NAMElib ${KELBON_TEMPLATE_PROJECT_NAME_SOURCES})

target_include_directories(KELBON_TEMPLATE_PROJECT_NAMElib PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")

target_link_libraries(KELBON_TEMPLATE_PROJECT_NAMElib PUBLIC
    ${CMAKE_THREAD_LIBS_INIT}
    anyanylib
    kelcorolib
    zallib
    benchmark::benchmark
)

add_executable(run_benchmark benchmark.cpp)

target_link_libraries(run_benchmark PUBLIC KELBON_TEMPLATE_PROJECT_NAMElib)

set_target_properties(KELBON_TEMPLATE_PROJECT_NAMElib run_benchmark
 PROPERTIES
	LINKER_LANGUAGE CXX
	CMAKE_CXX_STANDARD_REQUIRED ON
	CXX_STANDARD 20)

# generates launch.json, places compile_commands.json correctly for clangd
ccozy_on_configuration_end_vscode()
