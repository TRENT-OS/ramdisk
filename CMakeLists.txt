#
# RAM Disk driver
#
# Copyright (C) 2020-2021, HENSOLDT Cyber GmbH
#

cmake_minimum_required(VERSION 3.17)


#-------------------------------------------------------------------------------
#
# Declare RAM Disk CAmkES Component
#
# Parameters:
#
#   <name>
#       component instance name
#
function(RamDisk_DeclareCAmkESComponent
    name
)

    # Let pass an IMAGE parameter, which contains an RLE-encoded buffer with
    # a RamDisk image; this parameter is optional though
    cmake_parse_arguments(
        PARSE_ARGV
        1
        RAMDISK
        ""
        "IMAGE"
        ""
    )

    if(DEFINED RAMDISK_IMAGE)
        message(STATUS "Building RamDisk with image ${RAMDISK_IMAGE}")
    endif(DEFINED RAMDISK_IMAGE)

    DeclareCAmkESComponent(
        ${name}
        SOURCES
            ${CMAKE_CURRENT_FUNCTION_LIST_DIR}/RamDisk.c
            ${RAMDISK_IMAGE}
        C_FLAGS
            -Wall -Werror
        LIBS
            os_core_api
            lib_debug
            lib_utils
    )

endfunction()
