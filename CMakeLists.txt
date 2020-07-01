cmake_minimum_required(VERSION 3.2)
 project(blake2 C)

  set(CMAKE_POSITION_INDEPENDENT_CODE TRUE)
 set(CMAKE_C_STANDARD 11)    # force std=c11
 set(CMAKE_C_STANDARD_REQUIRED ON)
 set(CMAKE_C_EXTENSIONS OFF)

  include_directories(
   ${CMAKE_SOURCE_DIR}/include
 )

  add_library(blake2
   blake2s.c
   blake2b.c
   )

  include(GNUInstallDirs)

  install(TARGETS blake2 EXPORT blake2Config
   LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
   ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
   RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
   INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
   PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
   FRAMEWORK DESTINATION ${CMAKE_INSTALL_PREFIX}
   )
 install(
   DIRECTORY ${CMAKE_SOURCE_DIR}/include/blake2
   DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
 )
 install(
   EXPORT blake2Config
   DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}
 )
 export(
   TARGETS blake2
   FILE blake2Config.cmake
 )

  if (TESTING)
   enable_testing()
   add_executable(blake2_test test_main.c)
   add_test(NAME blake2_test COMMAND blake2_test)
   target_link_libraries(blake2_test blake2)
 endif ()