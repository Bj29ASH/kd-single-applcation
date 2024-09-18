cmake_minimum_required(VERSION 3.27)
project(KDSingleApplication VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(KDSingleApplication INTERFACE)

target_include_directories(KDSingleApplication
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/KDSingleApplication>
)

target_link_directories(KDSingleApplication
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib>
  $<INSTALL_INTERFACE:lib/KDSingleApplication>
)

target_link_libraries(KDSingleApplication
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib/kdsingleapplication.lib>
  $<INSTALL_INTERFACE:kdsingleapplication.lib>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/KDSingleApplicationConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/KDSingleApplicationConfig.cmake"
  INSTALL_DESTINATION share/KDSingleApplication
)

install(TARGETS KDSingleApplication
  EXPORT KDSingleApplicationTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/KDSingleApplication DESTINATION include)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/kdsingleapplication.lib"
  DESTINATION lib/KDSingleApplication
)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/bin/kdsingleapplication.dll"
  DESTINATION bin
)

install(
  EXPORT KDSingleApplicationTargets
  DESTINATION share/KDSingleApplication
  NAMESPACE KDSingleApplication::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/KDSingleApplicationConfig.cmake"
  DESTINATION share/KDSingleApplication
)