cmake_minimum_required(VERSION 3.16)

project(osgearth_0)

set(TARGET_NAME ${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_DEBUG_POSTFIX d)

set(IMPORT_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/import/include)
set(IMPORT_LIB_DIR     ${CMAKE_SOURCE_DIR}/import/lib)

set(BIN_DIR         ${PROJECT_BINARY_DIR}/bin)
set(STATIC_LIB_DIR  ${PROJECT_BINARY_DIR}/lib/static)
set(DYNAMIC_LIB_DIR ${PROJECT_BINARY_DIR}/lib/dynamic)
set(PDB_DIR         ${PROJECT_BINARY_DIR}/pdb)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BIN_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${STATIC_LIB_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${DYNAMIC_LIB_DIR})
set(CMAKE_PDB_OUTPUT_DIRECTORY     ${PDB_DIR})

set(INCLUDE_DIR                 ${CMAKE_SOURCE_DIR}/include)
set(SOURCE_DIR                  ${CMAKE_SOURCE_DIR}/source)
set(EXPORT_STATIC_LIBRARY_NAME  ${TARGET_NAME}_static_lib)
set(EXPORT_DYNAMIC_LIBRARY_NAME ${TARGET_NAME}_dynamic_lib)

add_executable(${TARGET_NAME} ${SOURCE_DIR}/main.cpp)

target_include_directories(${TARGET_NAME} PUBLIC ${IMPORT_INCLUDE_DIR})
target_include_directories(${TARGET_NAME} PUBLIC ${INCLUDE_DIR})

target_link_directories(${TARGET_NAME} PUBLIC ${IMPORT_LIB_DIR})

find_library(osg       NAMES libosg.so       PATHS /lib/x86_64-linux-gnu REQUIRED)
find_library(osgDB     NAMES libosgDB.so     PATHS /lib/x86_64-linux-gnu REQIORED)
find_library(osgViewer NAMES libosgViewer.so PATHS /lib/x86_64-linux-gnu REQIORED)
find_library(osgGA     NAMES libosgGA.so     PATHS /lib/x86_64-linux-gnu REQIORED)
find_library(osgEarth  NAMES libosgEarth.so  PATHS /usr/local/lib64      REQUIRED)

target_link_libraries(${TARGET_NAME} PRIVATE osg)
target_link_libraries(${TARGET_NAME} PRIVATE osgDB)
target_link_libraries(${TARGET_NAME} PRIVATE osgViewer)
target_link_libraries(${TARGET_NAME} PRIVATE osgGA)
target_link_libraries(${TARGET_NAME} PRIVATE osgEarth)
