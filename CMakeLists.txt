cmake_minimum_required(VERSION 3.16)
project(Troitsa VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Исходники интерпретатора
set(TROITSA_SOURCES
    src/token.cpp
    src/lexer.cpp
    src/tree.cpp
    src/analyzer.cpp
    src/semantics.cpp
    src/interpreter.cpp
)

# Библиотека
add_library(troitsa STATIC ${TROITSA_SOURCES})
target_include_directories(troitsa PUBLIC ${CMAKE_SOURCE_DIR}/src)

# Исполняемый файл
add_executable(troitsa-cli src/main.cpp)
target_link_libraries(troitsa-cli troitsa)

# Установка
install(TARGETS troitsa-cli DESTINATION bin)
install(DIRECTORY examples/ DESTINATION share/troitsa/examples)

message(STATUS "")
message(STATUS "=== Троица ===")
message(STATUS "Версия: ${PROJECT_VERSION}")
message(STATUS "")
