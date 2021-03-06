cmake_minimum_required(VERSION 3.15)

set(BRCXXC_VERSON "\"3.1.1\"")
project(brcxxc VERSION ${BRCXXC_VERSION})

add_executable(brcxxc src/brcxxc.cpp)
set_target_properties(brcxxc PROPERTIES CXX_STANDARD 17)

if ((CMAKE_CXX_COMPILER_ID STREQUAL "GNU") )
# AND ( CMAKE_CXX_COMPILER_VERSION VERSION_LESS 8.0)
# add this when they finally fix it
  target_link_libraries(brcxxc stdc++fs)
endif()

install(TARGETS brcxxc RUNTIME DESTINATION bin)

if (CMAKE_SYSTEM_NAME STREQUAL "Linux")
  install(FILES doc/brcxxc.1 DESTINATION man/man1)
endif()


target_compile_definitions(brcxxc PRIVATE BRCXXC_VERSION="\"${BRCXXC_VERSION}\"")

#set (CPACK_PACKAGE_NAME "Binary Resources for C++ Compiler")
set (CPACK_PACKAGE_VENDOR "RPNX")
set (CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_LIST_DIR}/README.md")
set (CPACK_PACKAGE_DESCRIPTION_SUMMARY "A compiler that converts arbitrary data into C++ objects")
set (CPACK_PACKAGE_VERSION ${BRCXXC_VERSION})
set (CPACK_RPM_PACKAGE_URL "https://rpnx.net/")
#set (CPACK_SYSTEM_NAME "${CMAKE_SYSTEM_NAME}")
#set (CPACK_PACKAGE_FILE_NAME "brcxxc-${CPACK_PACKAGE_VERSION}-${CPACK_SYSTEM_NAME}")
set (CPACK_PACKAGE_CONTACT "Ryan P. Nicholl <rnicholl@protonmail.com>")
set (CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)
set (CPACK_NSIS_MODIFY_PATH ON)

include (CPack)
