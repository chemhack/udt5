file(GLOB_RECURSE SRC *.cpp *.cxx *.cc *.C *.c *.h *.hpp)

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

add_compile_options("-DOSX")
add_compile_options("-DAMD64")

endif()

add_library(udt STATIC ${SRC})

if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")

add_definitions("-DWIN32")
add_definitions("-DUDT_EXPORTS")
target_link_libraries(udt ws2_32 kernel32 user32)

endif()


if(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Windows")

target_link_libraries(udt pthread)
set(CMAKE_CXX_FLAGS "-fPIC -Wall -finline-functions -O3 -fno-strict-aliasing -fvisibility=hidden -std=c++11 -stdlib=libc++")

endif()