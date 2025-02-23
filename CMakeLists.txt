cmake_minimum_required(VERSION 3.0.0)
project(SSD1306 VERSION 0.1.0)

include(CTest)
enable_testing()

add_library(
    ${PROJECT_NAME} 
    ${PROJECT_SOURCE_DIR}/src/SSD1306.cpp 
    ${PROJECT_SOURCE_DIR}/src/Graphic.cpp 
    ${PROJECT_SOURCE_DIR}/src/TextBox.cpp
)

if (NOT TARGET I2C)
    add_subdirectory (${PROJECT_SOURCE_DIR}/lib/I2C)
endif()

target_include_directories(
    ${PROJECT_NAME} INTERFACE 
    ${PROJECT_SOURCE_DIR}/lib/I2C
)

target_include_directories(
    ${PROJECT_NAME} PUBLIC
    ${PROJECT_SOURCE_DIR}/include 
    ${PROJECT_SOURCE_DIR}/fonts
)

target_link_libraries(${PROJECT_NAME} I2C)

target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_17)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
