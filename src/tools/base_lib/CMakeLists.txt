ADD_LIBRARY(
    tools_base STATIC
    CryptoHelper.cpp
    linux/CryptoHelperLinux.cpp
)

target_link_libraries(
     tools_base
     ${EXTERNAL_LIBS}
)
