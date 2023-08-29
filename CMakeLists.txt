cmake_minimum_required(VERSION 3.27)
project(pacman-demo)

set(CMAKE_CXX_STANDARD 20)

#add_executable(pacman-demo src/main.cpp src/engine.cpp headers/engine.hpp src/draw.cpp src/input.cpp src/snakesection.cpp headers/snakesection.hpp src/update.cpp src/apple.cpp headers/apple.hpp src/wall.cpp headers/wall.hpp)
add_executable(pacman-demo src/main.cpp)

include_directories(headers /usr/include c:/sfml/include)

set(SFML_ROOT c:/sfml)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake_modules")
find_package(SFML REQUIRED system window graphics)
if (SFML_FOUND)
    include_directories(${SFML_INCLUDE_DIR})
    target_link_libraries(pacman-demo ${SFML_LIBRARIES})
endif()

file(COPY assets DESTINATION ${CMAKE_BINARY_DIR})

# Copy dlls to build directory
if(WIN32)
    file(GLOB BINARY_DEP_DLLS "${SFML_INCLUDE_DIR}/../bin/*.dll")
    file(COPY ${BINARY_DEP_DLLS} DESTINATION ${CMAKE_BINARY_DIR})
    file(GLOB MINGW_DEP_DLLS "C:/msys64/mingw64/bin/*.dll")
    file(COPY ${MINGW_DEP_DLLS} DESTINATION ${CMAKE_BINARY_DIR})
endif()
