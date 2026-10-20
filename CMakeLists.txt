cmake_minimum_required(VERSION 3.28)
project(SFML_ECS_Networking LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

include(FetchContent)
FetchContent_Declare(
  SFML
  GIT_REPOSITORY https://github.com/SFML/SFML.git
  GIT_TAG 3.0.0
  GIT_SHALLOW ON
  EXCLUDE_FROM_ALL SYSTEM)
FetchContent_MakeAvailable(SFML)

# cmake -S . -B build -G Ninja
add_executable(
  ${PROJECT_NAME} "SFML-ECS-Networking/main.cpp" "SFML-ECS-Networking/game.cpp"
                  "SFML-ECS-Networking/Tank.cpp")

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
target_link_libraries(${PROJECT_NAME} PRIVATE SFML::Graphics SFML::Network)
target_include_directories(${PROJECT_NAME} PRIVATE entt)
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT
                                                            ${PROJECT_NAME})
