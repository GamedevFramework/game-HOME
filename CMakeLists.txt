cmake_minimum_required(VERSION 3.10)

project(HOME
  VERSION 0.1.0
)

include(GNUInstallDirs)

find_package(gf REQUIRED COMPONENTS graphics)
find_package(SFML REQUIRED COMPONENTS audio)
find_package(Box2D REQUIRED)

set(HOME_DATA_DIR "${CMAKE_INSTALL_PREFIX}/share/games/HOME")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/code/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h @ONLY)

add_executable(HOME
  code/main.cc
  code/local/BackgroundMusic.cc
  code/local/Backpack.cc
  code/local/DayNight.cc
  code/local/Hero.cc
  code/local/Map.cc
  code/local/Physics.cc
  code/local/ResourceManager.cc
  code/local/Singletons.cc
  code/local/Spaceship.cc
  code/local/SupplyManager.cc
  code/local/Timekeeper.cc
  code/local/Timer.cc
  code/local/Victory.cc
)

target_include_directories(HOME
  PRIVATE
    ${BOX2D_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/code
    ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(HOME
  PUBLIC
    gf::graphics
    sfml-audio
    ${BOX2D_LIBRARIES}
)

install(
  TARGETS HOME
  RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)

install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/data/HOME"
  DESTINATION "${CMAKE_INSTALL_DATAROOTDIR}/games"
)
