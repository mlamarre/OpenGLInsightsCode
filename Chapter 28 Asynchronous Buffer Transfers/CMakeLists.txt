cmake_minimum_required (VERSION 3.10)
project (async_vbo_transfers)
set (CMAKE_CXX_STANDARD 14)
set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/bin)
set(GLEW_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/ext)
set(GLEW_LIBRARY ${CMAKE_SOURCE_DIR}/lib/glew32.lib)
set(GLM_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/ext)
message (STATUS "GLM INCLUDE DIR: " ${GLM_INCLUDE_DIR})
find_package(GLEW REQUIRED)
add_definitions(-DGLEW_STATIC -DGLM_FORCE_SWIZZLE)
find_package(OpenGL REQUIRED COMPONENTS OpenGL)
if (MSVC)
	add_compile_options(/MP /wd4244 /wd4267 /wd4302 /wd4311 /wd4312 /wd4996 )
endif()
add_library(async_vbo_lib   src/renderer.cpp
                            src/scene.cpp
							src/base/glew.c
                            src/base/app.cpp
                            src/base/base_win.cpp
                            src/base/base.cpp
                            src/base/canvas.cpp
                            src/base/event.cpp
                            src/base/font.cpp
                            src/base/frame_context.cpp
                            src/base/hptimer_win.cpp
                            src/base/mutex.cpp
                            src/base/pixelfmt.cpp
                            src/base/thread_win.cpp)

include_directories(${GLM_INCLUDE_DIR})
include_directories(${CMAKE_SOURCE_DIR}/src)

add_executable(app_scenario1 src/app_scenario1.cpp src/main.cpp)
target_link_libraries(app_scenario1 async_vbo_lib OpenGL::GL)
target_compile_definitions(app_scenario1 PUBLIC APP_SCENARIO1)

add_executable(app_scenario2 src/app_scenario2.cpp src/main.cpp)
target_link_libraries (app_scenario2 async_vbo_lib OpenGL::GL)
target_compile_definitions(app_scenario2 PUBLIC APP_SCENARIO2)

add_executable(app_scenario3 src/app_scenario3.cpp src/main.cpp)
target_link_libraries (app_scenario3 async_vbo_lib OpenGL::GL)
target_compile_definitions(app_scenario3 PUBLIC APP_SCENARIO3)

add_executable(app_scenario4 src/app_scenario4.cpp src/main.cpp)
target_link_libraries (app_scenario4 async_vbo_lib OpenGL::GL)
target_compile_definitions(app_scenario4 PUBLIC APP_SCENARIO4)

add_executable(app_bw src/app_bw.cpp src/main.cpp)
target_link_libraries (app_bw async_vbo_lib OpenGL::GL)
target_compile_definitions(app_bw PUBLIC APP_BW)

install(TARGETS app_scenario1
				app_scenario2
				app_scenario3
				app_scenario4
				app_bw
		RUNTIME DESTINATION ${CMAKE_SOURCE_DIR}/bin)