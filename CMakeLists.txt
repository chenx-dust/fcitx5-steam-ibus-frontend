cmake_minimum_required(VERSION 3.10)
project(fcitx5-steam-ibus-frontend VERSION 0.0.1)

set(REQUIRED_FCITX_VERSION 5.1.14)

find_package(ECM REQUIRED 1.0.0)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
include(FeatureSummary)
include(GNUInstallDirs)
include(ECMSetupVersion)
include(ECMUninstallTarget)

find_package(Fcitx5Core ${REQUIRED_FCITX_VERSION} REQUIRED)
find_package(Fcitx5Module REQUIRED COMPONENTS DBus)
find_package(PkgConfig REQUIRED)

include("${FCITX_INSTALL_CMAKECONFIG_DIR}/Fcitx5Utils/Fcitx5CompilerSettings.cmake")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

add_fcitx5_addon(steamibusfrontend steamibusfrontend.cpp)
target_link_libraries(steamibusfrontend Fcitx5::Core Fcitx5::Module::DBus)
install(TARGETS steamibusfrontend DESTINATION "${FCITX_INSTALL_ADDONDIR}")
configure_file(steamibusfrontend.conf.in.in steamibusfrontend.conf @ONLY)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/steamibusfrontend.conf" DESTINATION "${FCITX_INSTALL_PKGDATADIR}/addon"
        COMPONENT config)
