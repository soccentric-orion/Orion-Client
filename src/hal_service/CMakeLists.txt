add_library(orion_hal_service STATIC
    HalServiceImpl.cc
)

target_include_directories(orion_hal_service PRIVATE
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_SOURCE_DIR}/../Orion-HAL/src
)

target_link_libraries(orion_hal_service PRIVATE
    orion_registry
    orion_hal_bridge
    orion_protos
    ${ORION_GRPC_LIBRARIES}
    protobuf::libprotobuf
    spdlog::spdlog
)
