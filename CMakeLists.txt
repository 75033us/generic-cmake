cmake_minimum_required(VERSION 3.6)
get_filename_component(TOP_PROJECT_NAME ${CMAKE_SOURCE_DIR} NAME)
project(${TOP_PROJECT_NAME})

file(GLOB_RECURSE SRC_FILES
        "*.c"
        "*.cpp"
        "*.cxx")

file(GLOB_RECURSE HEADER_FILES
	"*.h")

foreach(HEADER IN LISTS HEADER_FILES)
  get_filename_component(DIR ${HEADER} DIRECTORY)
  get_filename_component(PARENT ${DIR} DIRECTORY)
  list(APPEND HEADER_DIRS ${DIR} ${PARENT})
endforeach(HEADER)

list(REMOVE_DUPLICATES HEADER_DIRS)

foreach(DIR IN LISTS HEADER_DIRS)
  message(${DIR})
endforeach(DIR)

list(LENGTH HEADER_DIRS LEN)
message("TOTAL HEADER DIRS: " ${LEN})

include_directories(${HEADER_DIRS})

add_executable(${PROJECT_NAME} ${HEADER_FILES} ${SRC_FILES})
