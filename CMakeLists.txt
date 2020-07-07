cmake_minimum_required(VERSION 3.11)

project(Poly2Tri)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if (MSVC)
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /O2 /DNDEBUG")
else()
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -ggdb" )
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3 -march=native -DNDEBUG -flto")
endif()

add_library(poly2tri STATIC
	
	poly2tri/poly2tri.h
	
	poly2tri/common/shapes.h
	poly2tri/common/shapes.cc
	poly2tri/common/utils.h
	
	poly2tri/sweep/advancing_front.h
	poly2tri/sweep/advancing_front.cc
	poly2tri/sweep/cdt.h
	poly2tri/sweep/cdt.cc
	poly2tri/sweep/sweep.h
	poly2tri/sweep/sweep.cc
	poly2tri/sweep/sweep_context.h
	poly2tri/sweep/sweep_context.cc

)

target_include_directories(poly2tri PUBLIC ${CMAKE_CURRENT_LIST_DIR}/poly2tri)

target_link_libraries(poly2tri PUBLIC
		glad
)
