cmake_minimum_required(VERSION 3.16)
project(ChartAnalyzer CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(MSVC)
    add_compile_options(/source-charset:utf-8)
endif()

include(FetchContent)

FetchContent_Declare(
    nlohmann_json
    GIT_REPOSITORY https://github.com/nlohmann/json.git
    GIT_TAG        v3.11.3
    GIT_SHALLOW    TRUE
)
FetchContent_MakeAvailable(nlohmann_json)

add_executable(analyzer FN_diffGuesser.cpp)

target_link_libraries(analyzer PRIVATE nlohmann_json::nlohmann_json)

if(WIN32)
    target_link_libraries(analyzer PRIVATE wininet)
endif()
