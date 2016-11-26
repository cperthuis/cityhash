#-------------------
# cityhash

cmake_minimum_required (VERSION 3.5) 

macro(make_absolute files)
	set (_out)
	foreach(file ${${files}})
		get_filename_component(file_abs ${file} ABSOLUTE)	
		LIST(APPEND _out ${file_abs})
	endforeach()
	set (${files} ${_out})
endmacro()

macro(make_definitions definitions)
	set (_out)
	foreach(definition ${${definitions}})
		LIST(APPEND _out -D${definition})
	endforeach()
	set (${definitions} ${_out})
endmacro()


set (PROJ cityhash)

set (CITYHASH_SRC src/)
set (CITYHASH_INCLUDES ${CITYHASH_SRC})
make_absolute(CITYHASH_INCLUDES)

set (INCLUDES
	${CITYHASH_INCLUDES}
)
set (DEFINITIONS
	_CRT_SECURE_NO_WARNINGS
)
make_definitions(DEFINITIONS)

SET (CITYHASH_SRC
	${CITYHASH_ROOT}city.cc
	${CITYHASH_ROOT}city.h
)

add_library(${PROJ} ${CITYHASH_SRC})
set_target_properties(${PROJ} PROPERTIES INCLUDE_DIRECTORIES "${INCLUDES}")
target_compile_definitions(${PROJ} PUBLIC ${DEFINITIONS})

if (${MSVC})
add_compile_flags("/wd4267")
endif(${MSVC})