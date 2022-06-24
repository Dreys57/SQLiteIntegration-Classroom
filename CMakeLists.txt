cmake_minimum_required(VERSION 3.14)

project(SQLiteIntegration)

if(WIN32)
	add_compile_options("/std:c++latest")
endif(WIN32)
set(CMAKE_CXX_STANDARD 17)
enable_testing()

find_package(unofficial-sqlite3 CONFIG REQUIRED)
find_package(GTest CONFIG REQUIRED)

add_library(SQLib
	${CMAKE_CURRENT_SOURCE_DIR}/SQLib/SQLib.h
	${CMAKE_CURRENT_SOURCE_DIR}/SQLib/SQLib.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/SQLib/SQLiteImpl.h
	${CMAKE_CURRENT_SOURCE_DIR}/SQLib/SQLiteImpl.cpp
)

target_link_libraries(SQLib 
  PRIVATE
	sqlite3
)

add_executable(SQLibTest
	${CMAKE_CURRENT_SOURCE_DIR}/SQLibTest/main.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/SQLibTest/SQLibTest.h
	${CMAKE_CURRENT_SOURCE_DIR}/SQLibTest/SQLibTest.cpp
)

target_link_libraries(SQLibTest
  PRIVATE
	GTest::gtest
	SQLib
	unofficial::sqlite3::sqlite3
)
