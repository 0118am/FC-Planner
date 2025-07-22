cmake_minimum_required(VERSION 3.8)
project(quadrotor_msgs)

find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(Eigen3 REQUIRED)

set(msg_files
  "msg/AuxCommand.msg"
  "msg/Corrections.msg"
  "msg/Gains.msg"
  "msg/OutputData.msg"
  "msg/PositionCommand.msg"
  "msg/PPROutputData.msg"
  "msg/Serial.msg"
  "msg/SO3Command.msg"
  "msg/StatusData.msg"
  "msg/TRPYCommand.msg"
  "msg/Odometry.msg"
  "msg/PolynomialTrajectory.msg"
  "msg/PolynomialTraj.msg"
  "msg/PolynomialTrajGroup.msg"
  "msg/PolynomialMatrix.msg"
  "msg/TakeoffLand.msg"
  "msg/Px4ctrlDebug.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  DEPENDENCIES geometry_msgs nav_msgs
)

add_library(encode_msgs src/encode_msgs.cpp)
ament_target_dependencies(encode_msgs Eigen3)

target_include_directories(encode_msgs PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

add_library(decode_msgs src/decode_msgs.cpp)
ament_target_dependencies(decode_msgs Eigen3)

target_include_directories(decode_msgs PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

install(DIRECTORY include/
  DESTINATION include
)

install(TARGETS encode_msgs decode_msgs
  DESTINATION lib
)

ament_export_include_directories(include)
ament_export_libraries(encode_msgs decode_msgs)
ament_package()
