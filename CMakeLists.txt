
cmake_minimum_required(VERSION 3.5)
project(wsasync-client)

add_compile_options(-std=c++11)

find_package(Boost 1.69.0 COMPONENTS system thread)


if (Boost_FOUND)
  # From the offical documentation:
  # Add include directories to the build. [...] If the SYSTEM option is given,
  # the compiler will be told the directories are meant as system include
  # directories on some platforms (signalling this setting might achieve effects
  # such as the compiler skipping warnings [...])."
  include_directories (SYSTEM ${Boost_INCLUDE_DIR})

  # From the offical documentation:
  # "Specify directories in which the linker will look for libraries. [...] Note
  # that this command is rarely necessary. Library locations returned by
  # find_package() and find_library() are absolute paths. Pass these absolute
  # library file paths directly to the target_link_libraries() command. CMake
  # will ensure the linker finds them."
  #link_directories (${Boost_LIBRARY_DIRS})
endif ()

file(GLOB_RECURSE sources  src/*.cpp src/*.h)
add_executable(${PROJECT_NAME} ${sources})
target_link_libraries (${PROJECT_NAME} ${Boost_LIBRARIES})
