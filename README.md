# display
https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c  

https://blog.csdn.net/qq_21078557/article/details/83690226  
https://blog.csdn.net/zhaoyun_zzz/article/details/86496621  
https://blog.csdn.net/u014374031/article/details/73441577  
cmake_minimum_required (VERSION 3.5)


project (multiface)
set(CMAKE_CXX_STANDRD 11)
set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-Wno-deprecated -std=c++11 -pthread -O3")

#set where to exe code
set(MAIN_FILE main.cpp)
set(EXECUTABLE_OUTPUT_PATH ../)


#set the link dir
set(MULTI_LIBS /home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/lib)
set(MULTI_DIRS /home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include)

#set(InferenceEngine_DIR 

set(OpenCV_DIR /opt/intel/openvino/opencv/bin)
find_package(OpenCV REQUIRED)


set(OpenCV_INCLUDE_DIRS /opt/intel/openvino/opencv/include/)
#set(OpenCV_LIBS /opt/intel/openvino/opencv/lib/)
#find inferenceengine
find_package(InferenceEngine REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})          # ${MULTI_DIRS})
include_directories(${InferenceEngine_INCLUDE_DIRS})


include_directories(/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/src/extension
/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/include
/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/samples/common
/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/samples/common/format_reader
/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/samples/thirdparty
/opt/intel/openvino_2019.1.144/deployment_tools/inference_engine/samples/build/thirdparty/gflags/include )

link_directories(${MULTI_DIRS} ${OpenCV_LIBRARY_DIRS})


#include_directories(/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include/common 
#/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include/extension 
#/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include
#/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include /common  
#/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include/common/format_reader
#/home/ubtech/ubt_face/version1_openvino/MultiFaceTrack/project/include/include)

add_executable(multiface AgeCascade.cpp Classification.cpp FaceAttribute.cpp detectors.cpp
GenderCascade.cpp HungarianAlg.cpp main.cpp multiFaceTrack.cpp UbtFaceDetect.cpp)
target_link_libraries(multiface ${OpenCV_LIBS} IE::ie_cpu_extension ${InferenceEngine_LIBRARIES} dl)
