cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")

find_library(log-lib log)

add_library(native-lib SHARED native-lib.cpp)
add_library(rust-lib STATIC IMPORTED)

set_property(TARGET rust-lib PROPERTY IMPORTED_LOCATION_DEBUG ${CMAKE_CURRENT_LIST_DIR}/app/target/i686-linux-android/debug/libapp.a)
set_property(TARGET rust-lib PROPERTY IMPORTED_LOCATION_RELEASE ${CMAKE_CURRENT_LIST_DIR}/app/target/i686-linux-android/release/libapp.a)

target_link_libraries(native-lib android rust-lib ${log-lib})