project(test_raylib)

include("../raylib/cmake/utils.cmake")

# Make sure raylib has been built
# TODO `build` directory should maybe be something else...
# TODO place somewhere else?
include_directories("../raylib/build/release")
include_directories("../raylib/src/external")
include_directories("../raylib/src/external/glfw/include")

set(EXECUTABLE_OUTPUT_PATH bin/${CMAKE_BUILD_TYPE})

## Add source files ##
	file (GLOB_RECURSE files ./*)
	file (GLOB_RECURSE source_files ../src/*)
## End of adding source files ##

## Remove main.cc files of modules ##
	FOREACH(item ${source_files})
		IF(${item} MATCHES "main.cc")
			LIST(REMOVE_ITEM source_files ${item})
		ENDIF(${item} MATCHES "main.cc")
		IF(${item} MATCHES "main.c")
			LIST(REMOVE_ITEM source_files ${item})
		ENDIF(${item} MATCHES "main.c")
		IF(${item} MATCHES "main.cpp")
			LIST(REMOVE_ITEM source_files ${item})
		ENDIF(${item} MATCHES "main.cpp")
	ENDFOREACH(item)
## End of removing main.cc files of modules ##

## Add executables ##
	add_executable (raylib_package ${files} ${source_files})
	link_libraries_to_executable(raylib_package)
## End of adding executables ##