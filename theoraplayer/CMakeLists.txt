cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project( theoraplayer )

#
# libtheoraplayer
#
# NOTE: Currently, the libyuv implementation causes large videos to be choppy on Linux.
# This workaround builds libtheoraplayer without libyuv by replacing -D_YUV_LIBYUV with -D_YUV_C
add_definitions(-D_USE_THEORA -D__SSSE3__ -DTHEORAVIDEO_EXPORTS -D_YUV_C -D_LIB -D_LINUX -DTHEP_POSIX)
#add_definitions(-D_USE_THEORA -D__SSSE3__ -DTHEORAVIDEO_EXPORTS -D_YUV_LIBYUV -D_LIB -D_LINUX)

include_directories(
        "${CMAKE_CURRENT_LIST_DIR}/../ogg/include"
        "${CMAKE_CURRENT_LIST_DIR}/../theora/include"
        "${CMAKE_CURRENT_LIST_DIR}/../vorbis/include"
        "${CMAKE_CURRENT_LIST_DIR}/include/theoraplayer"
        "${CMAKE_CURRENT_LIST_DIR}/src/"
        "${CMAKE_CURRENT_LIST_DIR}/src/formats/"
        "${CMAKE_CURRENT_LIST_DIR}/src/YUV/"
        "${CMAKE_CURRENT_LIST_DIR}/src/YUV/libyuv/include"
)

aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src THEORAPLAYER_SRC_DIR1)
aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src/formats/Theora THEORAPLAYER_SRC_DIR2)
aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src/YUV THEORAPLAYER_SRC_DIR3)
aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src/YUV/C THEORAPLAYER_SRC_DIR4)
aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src/YUV/libyuv THEORAPLAYER_SRC_DIR5)
aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src/YUV/libyuv/src THEORAPLAYER_SRC_DIR6)


add_library (
    theoraplayer
        SHARED
            ${THEORAPLAYER_SRC_DIR1}
            ${THEORAPLAYER_SRC_DIR2}
            ${THEORAPLAYER_SRC_DIR3}
            ${THEORAPLAYER_SRC_DIR4}
            ${THEORAPLAYER_SRC_DIR5}
            ${THEORAPLAYER_SRC_DIR6}
)

