add_library(orion_hal_bridge STATIC ResultSerializer.cc
) target_include_directories(orion_hal_bridge PRIVATE ${CMAKE_SOURCE_DIR}/src ${CMAKE_SOURCE_DIR}/../Orion-HAL/src
) target_link_libraries(orion_hal_bridge PRIVATE orion_protos spdlog::spdlog
)
