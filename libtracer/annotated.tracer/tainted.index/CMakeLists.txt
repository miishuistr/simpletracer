set(LIBRARY_NAME taintedindex)

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
  TaintedIndex.cpp
  TrackingExecutor.cpp
)

install (TARGETS ${LIBRARY_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)
