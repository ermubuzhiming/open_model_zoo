# Copyright (C) 2018-2019 Intel Corporation
# SPDX-License-Identifier: Apache-2.0
#

file(GLOB SRC_FILES ./*.cpp)
file(GLOB H_FILES ./*.h)

ie_add_sample(NAME segmentation_demo
              SOURCES ${SRC_FILES}
              HEADERS ${H_FILES}
              DEPENDENCIES monitors models pipelines
              OPENCV_DEPENDENCIES highgui videoio imgproc)
