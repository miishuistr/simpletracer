## tracer CmakeLists.txt

set(LIBRARY_NAME tracer)

if(WIN32)
set(FLAGS_CROSS "-D_cdecl=\"__cdecl\" \
	-D_stdcall=\"__stdcall\"")
else(WIN32)
set(FLAGS_CROSS "-D_cdecl=\"__attribute__((cdecl))\" \
	-D_stdcall=\"__attribute__((stdcall))\"")
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -m32 -std=c++11 ${FLAGS_CROSS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -m32 -std=c++11 ${FLAGS_CROSS}")

include_directories(${Z3_ROOT}/include)

add_library(${LIBRARY_NAME} STATIC
  utils.cpp
  basic.observer.cpp
  simple.tracer/simple.tracer.cpp
  annotated.tracer/annotated.tracer.cpp)

add_subdirectory(./annotated.tracer/tainted.index)
add_subdirectory(./annotated.tracer/z3.executor)

install (TARGETS ${LIBRARY_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)
