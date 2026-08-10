add_library(orion_log STATIC LogCollector.cc
) target_include_directories(orion_log PRIVATE ${CMAKE_SOURCE_DIR}/src
) target_link_libraries(orion_log PRIVATE orion_protos spdlog::spdlog
)
