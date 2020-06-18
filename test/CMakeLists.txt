function(add_googletest)
	set(BUILD_GMOCK OFF CACHE BOOL "")
	set(BUILD_GTEST ON CACHE BOOL "")
	set(INSTALL_GMOCK OFF CACHE BOOL "")
	set(INSTALL_GTEST ON CACHE BOOL "")
    set(gtest_force_shared_crt ON CACHE BOOL "Force gtest to used shared VC++ CRT")
	add_subdirectory(googletest)
	include_directories("${gtest_SOURCE_DIR}/include")
endfunction(add_googletest)
add_googletest()

find_package (Threads)

SET(SOURCES
	"val.test.cpp"
)

source_group("src" FILES ${SOURCES})

add_executable(val_test ${SOURCES})
target_link_libraries(val_test gtest gtest_main ${CMAKE_THREAD_LIBS_INIT})
set_property(TARGET val_test PROPERTY CXX_STANDARD 17)
set_property(TARGET val_test PROPERTY CXX_STANDARD_REQUIRED ON)

add_test(NAME val_test COMMAND "$<TARGET_FILE:val_test>")
