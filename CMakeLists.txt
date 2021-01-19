cmake_minimum_required(VERSION 3.6.0)

project(ZStream
  VERSION 1.0.4
  DESCRIPTION "A C++ ZLib wrapper"
)

##
##  zlib (use prebuild libraries)
##
find_package(zlib CONFIG REQUIRED)

## add library definistions
add_library(zstr INTERFACE)
target_include_headers(zstr INTERFACE ${CMAKE_CURRENT_LIST_DIR}/include)
set_target_properties(zstr PROPERTIES
        CXX_STANDARD 11
        CXX_EXTENSIONS OFF)

target_link_libraries(zstr INTERFACE Zlib::zlibstatic)

## add install configuration
install(TARGETS zstr EXPORT zstrConfig)
install(FILES ${CMAKE_CURRENT_LIST_DIR}/include DESTINATION include/zstr)

export(TARGETS zstr FILE zstrConfig.cmake NAMESPACE ZStream::)

install(EXPORT zstrConfig DESTINATION share/zstr NAMESPACE ZStream::)