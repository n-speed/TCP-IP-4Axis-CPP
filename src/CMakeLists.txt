# Minimum CMake Version Required
cmake_minimum_required(VERSION 3.0)

# Project Name
project(DobotTcpDemo)

# Using C++ 17
set(CMAKE_CXX_STANDARD 17)
# Build type using release
set(CMAKE_BUILD_TYPE Realease)

# Defining executable name and adding source files for compile
add_executable(DobotTcpDemo DobotTcpDemo.cpp api/BitConverter.cpp api/Dashboard.cpp api/DobotClient.cpp api/DobotMove.cpp api/ErrorInfoBean.cpp api/ErrorInfoHelper.cpp api/Feedback.cpp)

# Linking to threads/pthreads (although modm isn't used...)
find_package(Threads REQUIRED)
target_link_libraries(DobotTcpDemo Threads::Threads)