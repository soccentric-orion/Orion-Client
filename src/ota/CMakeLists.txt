add_library(orion_ota STATIC OtaClient.cc
) target_include_directories(orion_ota PRIVATE ${CMAKE_SOURCE_DIR}/src
) target_link_libraries(orion_ota PRIVATE orion_protos ${ORION_GRPC_LIBRARIES} spdlog::spdlog
)
