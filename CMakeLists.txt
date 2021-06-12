cmake_minimum_required(VERSION 3.20)
project(crypto LANGUAGES C)

include(CheckIncludeFile)
include(CheckTypeSize)

set(crypto_headers
    aes.h
    arcfour.h
    base64.h
    blowfish.h
    des.h
    md2.h
    md5.h
    rot-13.h
    sha1.h
    sha256.h
)
# check header and type
check_include_file("stddef.h" HAVE_STDDEF_H)
check_include_file("stdlib.h" HAVE_STDLIB_H)
check_include_file("memory.h" HAVE_MEMORY_H)
check_include_file("string.h" HAVE_STRING_H)
check_type_size("size_t" TYPE_SIZE_T)
option(BUILD_DLL_LIB "if you want build .dll file or .o file, your can open this option" ON)
option(BUILD_STATIC_FILE "if you want build a static lib, that file extension like .a,you can open this options" OFF)
option(ISNTALL_IN_SYSTEM "" OFF)

if(NOT ${ISNTALL_IN_SYSTEM})
    set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/crypto")
endif()

include_directories(./)

if(MSVC)
    set(CMAKE)
else()
endif()


if(${BUILD_DLL_LIB})
    add_library(aes SHARED aes.c)
    add_library(arcfour SHARED arcfour.c)
    add_library(base64 SHARED base64.c)
    add_library(blowfish SHARED blowfish.c)
    add_library(des SHARED des.c)
    add_library(md2 SHARED md2.c)
    add_library(md5 SHARED md5.c)
    add_library(rot-13 SHARED rot-13.c)
    add_library(sha1 SHARED sha1.c)
    add_library(sha256 SHARED sha256.c)
endif()

if(${BUILD_STATIC_FILE})
    add_library(aes STATIC aes.c)
    add_library(arcfour STATIC arcfour.c)
    add_library(base64 STATIC base64.c)
    add_library(blowfish STATIC blowfish.c)
    add_library(des STATIC des.c)
    add_library(md2 STATIC md2.c)
    add_library(md5 STATIC md5.c)
    add_library(rot-13 STATIC rot-13.c)
    add_library(sha1 STATIC sha1.c)
    add_library(sha256 STATIC sha256.c)
    # target_link_libraries(crypto "${PROJECT_SOURCE_DIR}/libaes.a")
endif()

# install lib
install(TARGETS aes LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS arcfour LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS base64 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS blowfish LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS des LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS md2 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS md5 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS rot-13 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS sha1 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(TARGETS sha256 LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(FILES ${crypto_headers} DESTINATION "${CMAKE_INSTALL_PREFIX}/include/crypto")