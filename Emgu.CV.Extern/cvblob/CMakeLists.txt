# --------------------------------------------------------
#  Copyright (C) 2004-2011 by EMGU. All rights reserved.
# 
#  CMake file for cvextern. See root CMakeLists.txt
#
# ----------------------------------------------------------------------------
project(cvblob)

INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/../../opencv/include/opencv")
INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/../../opencv/include")

SET(OPENCV_MODULES_DIR "${PROJECT_SOURCE_DIR}/../../opencv/modules")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/core/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/imgproc/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/ml/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/calib3d/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/objdetect/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/features2d/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/legacy/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/contrib/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/highgui/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/flann/include")
INCLUDE_DIRECTORIES("${OPENCV_MODULES_DIR}/video/include")

############################### CVBLOB START ########################
file(GLOB CVBLOB_SRCS "libcvblob/*.cpp")
file(GLOB CVBLOB_HDRS "libcvblob/*.h*")

LIST(APPEND cvblob_srcs ${CVBLOB_SRCS})
LIST(APPEND cvblob_hdrs ${CVBLOB_HDRS})
############################### CVBLOB END ##########################

source_group("Src" FILES ${cvblob_srcs})
source_group("Include" FILES ${cvblob_hdrs})
set(the_target ${PROJECT_NAME})
add_library(${the_target} STATIC ${cvblob_srcs} ${cvblob_hdrs})

# For dynamic link numbering convenions
set_target_properties(${the_target} PROPERTIES
    OUTPUT_NAME "${the_target}"
    )

if(ENABLE_SOLUTION_FOLDERS)
    set_target_properties(${the_target} PROPERTIES FOLDER "3rdparty")
endif() 

ADD_DEPENDENCIES(${the_target} 
  opencv_core opencv_calib3d opencv_contrib opencv_features2d opencv_highgui opencv_imgproc opencv_legacy opencv_ml opencv_objdetect)

