cmake_minimum_required(VERSION 3.0)
project(damgard_jurik)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES damgard_jurik.h damgard_jurik.cpp)
add_library(damgard_jurik SHARED ${SOURCE_FILES})
target_link_libraries(damgard_jurik gmp)
#add_executable(damgard_jurik ${SOURCE_FILES})
#install(LIBRARY DESTINATION lib
#        RUNTIME DESTINATION bin
#        )
#install(FILES damgard_jurik.h DESTINATION include)
