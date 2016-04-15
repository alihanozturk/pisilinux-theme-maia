project(MaiaTheme)

cmake_minimum_required(VERSION 3.0.0 FATAL_ERROR)

include(WriteBasicConfigVersionFile)
include(FeatureSummary)

find_package(ECM 1.5.0 REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

# Set version
set(THEME_VERSION_MAJOR 0)
set(THEME_VERSION_MINOR 3)
set(THEME_VERSION_PATCH 2)
set(THEME_VERSION_STRING "${THEME_VERSION_MAJOR}.${THEME_VERSION_MINOR}.${THEME_VERSION_PATCH}")

find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS Plasma)
  
include(ECMInstallIcons)
include(KDEInstallDirs)
include(KDECMakeSettings)
include(KDECompilerSettings)
include(GenerateExportHeader)

add_subdirectory(icons)
add_subdirectory(maia)
add_subdirectory(wallpapers)

plasma_install_package(lookandfeel org.kde.maia.desktop look-and-feel lookandfeel)

install(DIRECTORY lookandfeel/contents/loginmanager/ DESTINATION ${CMAKE_INSTALL_PREFIX}/share/sddm/themes/maia PATTERN "README.txt" EXCLUDE)
install(DIRECTORY lookandfeel/contents/components DESTINATION ${CMAKE_INSTALL_PREFIX}/share/sddm/themes/maia PATTERN "README.txt" EXCLUDE)

INSTALL(FILES colors/Maia-Pisi.colors DESTINATION ${DATA_INSTALL_DIR}/color-schemes/)
if(EXISTS ${CMAKE_SOURCE_DIR}/po AND IS_DIRECTORY ${CMAKE_SOURCE_DIR}/po)
  find_package(KF5I18n CONFIG REQUIRED)
  ki18n_install(po)
endif()

feature_summary(WHAT ALL INCLUDE_QUIET_PACKAGES FATAL_ON_MISSING_REQUIRED_PACKAGES)
