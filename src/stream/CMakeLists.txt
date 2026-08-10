add_library(orion_stream STATIC
    StreamClient.cc
)

target_include_directories(orion_stream PRIVATE
    ${CMAKE_SOURCE_DIR}/src
)

target_link_libraries(orion_stream PRIVATE
    orion_protos
    ${ORION_GRPC_LIBRARIES}
    spdlog::spdlog
)
