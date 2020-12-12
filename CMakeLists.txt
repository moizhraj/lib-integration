cmake_minimum_required(VERSION 3.10)

project(iot-sample C)

set(CMAKE_C_STANDARD 99)

set(SOURCES
    main.c
)

ADD_LIBRARY(math_ops STATIC IMPORTED)
set_target_properties(math_ops PROPERTIES
    IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/libMATH_OPS_LIB.a
    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}/inc/math-ops"
)
ADD_LIBRARY(paho_mqtt STATIC IMPORTED)
set_target_properties(paho_mqtt PROPERTIES
    IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/libpaho-mqtt3a-static.a
    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}/inc/paho-mqtt"
)

include_directories(PUBLIC ${CMAKE_SOURCE_DIR}/inc)

add_executable("lib_integration"
    ${SOURCES}
)

TARGET_LINK_LIBRARIES("lib_integration" 
    math_ops
    paho_mqtt
)