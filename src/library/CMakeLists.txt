add_subdirectory("os")
add_subdirectory("base")
add_subdirectory("ini")
add_subdirectory("locate")


ADD_LIBRARY(licensecc_static STATIC
    license++.cpp
    LicenseReader.cpp
    pc-identifiers.c
)

target_link_libraries(
     licensecc_static
     ini
     locators
     os
     base
)
