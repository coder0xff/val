cmake_minimum_required (VERSION 3.10)
project(plange)
enable_testing()

find_package(Git)
if (GIT_FOUND)
	mark_as_advanced(
		FORCE
		git_executable
	)
	message(INFO " Initializing git submodules...")
	execute_process(
		COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
		WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
else()
	message(WARNING " Git was not found. Uninitialized git submodules must be initialized manually.")
endif()

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (HEADERS "val.hpp")
source_group("include" FILES ${HEADERS})

add_subdirectory(test)
