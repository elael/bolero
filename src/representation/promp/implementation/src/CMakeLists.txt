include_directories(${EIGEN3_INCLUDE_DIRS} .)
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()
set(HDRS BasisFunctions.h Trajectory.h promp.h)
set(SRCS BasisFunctions.cpp Trajectory.cpp promp.cpp)


add_library(promp SHARED ${SRCS} )

                         
install (TARGETS promp DESTINATION lib)
install (FILES ${HDRS} DESTINATION include/${PROJECT_NAME})
