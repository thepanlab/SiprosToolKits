add_executable(SiprosV3omp ${SRC_LIST} ${PROJECT_SOURCE_DIR}/openmp/main.cpp)

# target_compile_options(SiprosV3omp PUBLIC -ffast-math -march=native)
target_compile_options(SiprosV3omp PUBLIC -ffast-math)

if("${CMAKE_BUILD_TYPE}" STREQUAL "Debug")
    target_link_libraries(SiprosV3omp PUBLIC OpenMP::OpenMP_CXX profiler)
    target_compile_definitions(SiprosV3omp PUBLIC Gper)
else()
    # target_link_libraries(SiprosV3omp PUBLIC OpenMP::OpenMP_CXX)
    target_link_libraries(SiprosV3omp PUBLIC OpenMP::OpenMP_CXX gomp dl -static)
    if(DEFINED Ticktock)
        target_compile_definitions(SiprosV3omp PUBLIC Ticktock)
    endif()
endif()
