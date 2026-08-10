add_library(orion_run STATIC
    RunOrchestrator.cc
)

target_include_directories(orion_run PRIVATE
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_SOURCE_DIR}/../Orion-HAL/src
)

target_link_libraries(orion_run PRIVATE
    orion_hal_bridge
    orion_protos
    spdlog::spdlog
)
