cmake_minimum_required(VERSION 3.2...3.28)

project(
    SimpleToDoList
    Version 0.1
    DESCRIPTION "Simple ToDo List in c++"
    LANGUAGES CXX
)

if(CMAKE_PROJECT_NAME STREQUAL SIMPLE_TODO_LIST)

    set_property(GLOBAL PROPERTY USE_FOLDERS on)

    include(CTest)

    find_package(Doxygen)
    if(Doxygen_Found)
        add_subdirectory(docs)
    else()
        message(STATUS "Doxygen not found! Not able to build nice docs.")
    endif()   
    
endif()

include(FetchContent)

FetchContent_Declare(
    imGui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
)

FetchContent_MakeAvailable(imGui)

add_subdirectory(src)

add_subdirectory(app)

if((CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME OR MODERN_CMAKE_BUILD_TESTING)
 AND BUILD_TESTING)
    add_subdirectory(tests)
endif()    
