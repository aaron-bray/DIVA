# We only need to get OpenCV needed for the optional image display logic in some examples
find_package( OpenCV REQUIRED )
if( OpenCV_VERSION VERSION_LESS "2.4" )
  message( FATAL_ERROR "OpenCV version must be at least 2.4" )
endif()

set(SOURCE "darknet_detections.cpp")

include_directories(${OpenCV_INCLUDE_DIRS})
include_directories("${CMAKE_BINARY_DIR}")
include_directories("${CMAKE_SOURCE_DIR}/utils")
add_executable(darknet_detections ${SOURCE})
target_link_libraries(darknet_detections 
                      diva_utils
                      kwiversys
                      vital
                      vital_algo
                      vital_config
                      vital_logger
                      vital_util
                      vital_vpm
# The next 3 lines are needed for the optional image display logic in some examples
                      kwiver_algo_ocv
                      ${OpenCV_LIBS})
link_directories(${OpenCV_LIB_DIR})

if(WIN32)
  target_compile_definitions(darknet_detections PRIVATE YAML_CPP_DLL)
endif()