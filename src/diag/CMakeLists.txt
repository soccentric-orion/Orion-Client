add_library(orion_diag STATIC DiagSocket.cc
) target_include_directories(orion_diag PRIVATE ${CMAKE_SOURCE_DIR}/src
) target_link_libraries(orion_diag PRIVATE spdlog::spdlog
)
