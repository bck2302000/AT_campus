cmake_minimum_required(VERSION 2.8)
project(hanke_pison_image_transport)

find_package(catkin REQUIRED COMPONENTS cv_bridge image_transport message_generation sensor_msgs)

# add the resized image message
#add_message_files(DIRECTORY msg
#   FILES ResizedImage.msg
#)
generate_messages(DEPENDENCIES sensor_msgs)

catkin_package(CATKIN_DEPENDS cv_bridge image_transport message_runtime sensor_msgs)

find_package(OpenCV)

include_directories(include ${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})

# add the publisher example
add_executable(video_publisher src/video_publisher.cpp)
add_dependencies(video_publisher ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(video_publisher ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

add_executable(video_publisher_2 src/video_publisher_2.cpp)
add_dependencies(video_publisher_2 ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(video_publisher_2 ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

# add the subscriber example
add_executable(my_subscriber src/my_subscriber.cpp)
add_dependencies(my_subscriber ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(my_subscriber ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

# add the plugin example
#add_library(resized_publisher src/manifest.cpp src/resized_publisher.cpp src/#resized_subscriber.cpp)
#add_dependencies(resized_publisher ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
#target_link_libraries(resized_publisher ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})


# Mark executables and/or libraries for installation
install(TARGETS video_publisher my_subscriber #resized_publisher
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

#install(FILES resized_plugins.xml
#        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
#)
