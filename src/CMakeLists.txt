# ---------------------------------------------------------------------------
# src/CMakeLists.txt
# Adds each module as a static library then defines the main executable.
# Subdirectories are ordered leaf-first so inter-target references resolve.
# --------------------------------------------------------------------------- add_subdirectory(config)
add_subdirectory(diag)
add_subdirectory(spool)
add_subdirectory(stream)
add_subdirectory(hal_bridge)
add_subdirectory(registry)
add_subdirectory(ota)
add_subdirectory(log)
add_subdirectory(janitor)
add_subdirectory(run)
add_subdirectory(hal_service) # ---------------------------------------------------------------------------
# Main executable
# --------------------------------------------------------------------------- add_executable(orion-client main.cpp app.cpp
) target_include_directories(orion-client PRIVATE ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_SOURCE_DIR}/../Orion-HAL/src
) target_link_libraries(orion-client PRIVATE orion_config orion_diag orion_hal_bridge orion_hal_service orion_janitor orion_log orion_ota orion_registry orion_run orion_spool orion_stream orion_protos spdlog::spdlog tomlplusplus::tomlplusplus yaml-cpp::yaml-cpp SQLite::SQLite3 ${ORION_GRPC_LIBRARIES} protobuf::libprotobuf
) target_compile_definitions(orion-client PRIVATE ORION_CLIENT_VERSION="${PROJECT_VERSION}"
) set_compiler_warnings(orion-client)
