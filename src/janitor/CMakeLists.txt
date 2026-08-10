add_library(orion_janitor STATIC
    Janitor.cc
)

target_include_directories(orion_janitor PRIVATE
    ${CMAKE_SOURCE_DIR}/src
)

target_link_libraries(orion_janitor PRIVATE
    orion_protos
    spdlog::spdlog
)
