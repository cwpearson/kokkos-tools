kp_add_library(kp_perfetto_connector libperfetto-connector.cpp perfetto/perfetto.cc)
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    # this is third-party code, so we just disable some errors that pop up
    target_compile_options(kp_perfetto_connector PRIVATE -Wno-error=redundant-move)
endif()
target_include_directories(kp_perfetto_connector PRIVATE perfetto)

