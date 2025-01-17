# perfetto/perfetto.cc is third-party code, so we want to disable all warnings for it
add_library(perfetto_static STATIC perfetto/perfetto.cc)
set_target_properties(perfetto_static PROPERTIES POSITION_INDEPENDENT_CODE ON)
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    target_compile_options(perfetto_static PRIVATE -w)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    target_compile_options(perfetto_static PRIVATE /w)
endif()

kp_add_library(kp_perfetto_connector libperfetto-connector.cpp)
target_link_libraries(kp_perfetto_connector PRIVATE perfetto_static)

# mark as system so we don't get warnings from perfetto.h either
target_include_directories(kp_perfetto_connector PRIVATE SYSTEM perfetto)
