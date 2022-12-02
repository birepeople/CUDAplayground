cmake_minimum_required(VERSION 3.18)
project(CUDAplayground LANGUAGES C CXX CUDA)

# set C++14 standard supported
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
#set build directory structure
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/${CMAKE_BUILD_TYPE})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib/${CMAKE_BUILD_TYPE})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/${CMAKE_BUILD_TYPE})

# add cuda
find_package(CUDA REQUIRED)
if(CUDA_FOUND)
    include_directories(${CUDA_INCLUDE_DIRS})
    link_directories(${CUDA_TOOLKIT_ROOT_DIR}/lib64)
    link_libraries(${CUDA_LIBRARIES})
else()
    message("Cuda not found")
endif()

# add thrust
find_package(Thrust REQUIRED CONFIG)
thrust_create_target(Thrust)

# add external
add_subdirectory(external)

# add src
add_subdirectory(src)

# add example
add_subdirectory(example)

