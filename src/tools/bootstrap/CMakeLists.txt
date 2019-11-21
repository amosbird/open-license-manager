add_executable(
    bootstrap
    bootstrap.cpp
    )

SET_TARGET_PROPERTIES(bootstrap PROPERTIES LINK_SEARCH_END_STATIC OFF)
target_link_libraries(
    bootstrap
    tools_base
    ${EXTERNAL_LIBS}
    )

add_custom_target(private_key DEPENDS "${CMAKE_SOURCE_DIR}/private-key.h")
add_custom_target(public_key DEPENDS "${CMAKE_SOURCE_DIR}/public-key.h")
