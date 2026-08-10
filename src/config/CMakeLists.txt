add_library(orion_config STATIC client_config.cpp client_id.cpp
) target_include_directories(orion_config PRIVATE ${CMAKE_SOURCE_DIR}/src
) target_link_libraries(orion_config PRIVATE spdlog::spdlog tomlplusplus::tomlplusplus yaml-cpp::yaml-cpp
)
