cmake_minimum_required(VERSION 3.10)
project(ruckig)

set(CMAKE_CXX_STANDARD 17)

if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
    message("${PROJECT_NAME}: You did not request a specific build type: Choosing 'Release' for maximum performance")
    set(CMAKE_BUILD_TYPE Release)
endif()

include_directories(include)
find_package(ament_cmake REQUIRED)

set(RUCKIG_DEPS
    src/ruckig/brake.cpp
    src/ruckig/position_first_step1.cpp
    src/ruckig/position_first_step2.cpp
    src/ruckig/position_second_step1.cpp
    src/ruckig/position_third_step1.cpp
    src/ruckig/position_second_step2.cpp
    src/ruckig/position_third_step2.cpp
    src/ruckig/velocity_second_step1.cpp
    src/ruckig/velocity_second_step2.cpp
    src/ruckig/velocity_third_step1.cpp
    src/ruckig/velocity_third_step2.cpp
)

add_library(ruckig ${RUCKIG_DEPS})
ament_target_dependencies(ruckig ament_cmake)

install(TARGETS ruckig
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY include/
  DESTINATION include/
)

ament_export_include_directories(include)
ament_export_libraries(ruckig)
ament_package()