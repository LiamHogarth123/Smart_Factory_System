cmake_minimum_required(VERSION 3.5)
project(path_planner_setup)

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(marker_msgs REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)
find_package(OpenCV REQUIRED)  # Find OpenCV package
find_package(nlohmann_json REQUIRED)


# Add executables and link libraries
add_executable(prm_creation 
  src/prm_creation.cpp
  src/main.cpp
  # src/task_allocation.cpp
  src/prm2.cpp
  # src/turtlebot_sensorprocessing.cpp
  # src/turtlebot_control_cal.cpp
)

# target_link_libraries(${PROJECT_NAME} nlohmann_json::nlohmann_json)

# Link the executable to the necessary libraries
ament_target_dependencies(
  prm_creation
  rclcpp
  geometry_msgs
  nav_msgs
  sensor_msgs
  marker_msgs
  tf2_geometry_msgs
)

# Link OpenCV libraries to the executable
target_link_libraries(prm_creation
  ${OpenCV_LIBS}
  nlohmann_json::nlohmann_json
)

# Install the executable
install(TARGETS
prm_creation
  DESTINATION lib/${PROJECT_NAME})

# Install launch files
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}/)

ament_package()
