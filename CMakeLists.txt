cmake_minimum_required(VERSION 2.8.2)

project(TinyXML)

set(SRCS
    tinyxml.cpp
    tinyxmlparser.cpp
    xmltest.cpp
    tinyxmlerror.cpp
    tinystr.cpp
)

set(HDRS tinyxml.h tinystr.h)

add_library(tinyxml ${SRCS})
target_include_directories(tinyxml PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

install(TARGETS tinyxml
    EXPORT ${PROJECT_NAME}Targets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(FILES ${HDRS} DESTINATION include/)

install(EXPORT ${PROJECT_NAME}Targets
    DESTINATION lib/cmake/${PROJECT_NAME}
    NAMESPACE TinyXML::
    FILE ${PROJECT_NAME}Targets.cmake
)

configure_file(cmake/pkgConfig.cmake.in ${PROJECT_NAME}Config.cmake @ONLY)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    DESTINATION lib/cmake/${PROJECT_NAME}
)
