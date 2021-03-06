set(MOVEIT_LIB_NAME moveit_depth_image_octomap_updater)

add_library(${MOVEIT_LIB_NAME}_core src/depth_image_octomap_updater.cpp)
set_target_properties(${MOVEIT_LIB_NAME}_core PROPERTIES VERSION "${${PROJECT_NAME}_VERSION}")
ament_target_dependencies(${MOVEIT_LIB_NAME}_core
  rclcpp
  moveit_core
  image_transport
  sensor_msgs
  tf2
  tf2_geometry_msgs
  geometric_shapes
  moveit_ros_occupancy_map_monitor
  Boost
)
target_link_libraries(${MOVEIT_LIB_NAME}_core moveit_lazy_free_space_updater moveit_mesh_filter)

add_library(${MOVEIT_LIB_NAME} src/updater_plugin.cpp)
set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${${PROJECT_NAME}_VERSION}")
ament_target_dependencies(${MOVEIT_LIB_NAME}
  rclcpp
  moveit_core
  image_transport
  sensor_msgs
  tf2
  tf2_geometry_msgs
  geometric_shapes
  moveit_ros_occupancy_map_monitor
  Boost
  pluginlib
)
target_link_libraries(${MOVEIT_LIB_NAME} ${MOVEIT_LIB_NAME}_core)

install(TARGETS ${MOVEIT_LIB_NAME}_core ${MOVEIT_LIB_NAME}
        EXPORT  ${MOVEIT_LIB_NAME}_core ${MOVEIT_LIB_NAME}
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)
