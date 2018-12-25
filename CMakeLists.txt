cmake_minimum_required(VERSION 2.8.3)
project(libcreate)

find_package(catkin REQUIRED)
find_package(Boost REQUIRED COMPONENTS system thread)
find_package(Threads REQUIRED)

catkin_package(INCLUDE_DIRS include LIBRARIES ${PROJECT_NAME})

# Specify locations of header files
include_directories(include SYSTEM ${catkin_INCLUDE_DIRS})

# Declare cpp library
add_library(${PROJECT_NAME}
  src/create.cpp
  src/serial.cpp
  src/serial_stream.cpp
  src/serial_query.cpp
  src/data.cpp
  src/packet.cpp
  src/types.cpp
)
add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${Boost_LIBRARIES})

## Mark library for installation
install(TARGETS ${PROJECT_NAME}
    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
## Mark cpp header files for installation
install(DIRECTORY include/create/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
    FILES_MATCHING PATTERN "*.h"
    PATTERN ".svn" EXCLUDE
)

