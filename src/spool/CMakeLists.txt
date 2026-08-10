add_library(orion_spool STATIC Spool.cc
) target_include_directories(orion_spool PRIVATE ${CMAKE_SOURCE_DIR}/src
) target_link_libraries(orion_spool PRIVATE orion_protos SQLite::SQLite3 spdlog::spdlog
)
