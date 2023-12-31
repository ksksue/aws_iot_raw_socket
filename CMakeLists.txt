#
# Copyright (c) 2020 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-Nordic-5-Clause
#

cmake_minimum_required(VERSION 3.20.0)

set(DTC_OVERLAY_FILE "myboard.overlay")
set(CONF_FILE "prj.conf")
list(APPEND CONF_FILE "myprj.conf")

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(aws_iot)

# NORDIC SDK APP START
target_sources(app PRIVATE src/main.c)
# NORDIC SDK APP END

zephyr_include_directories(src)

# Make folder containing certificates global so that it can be located by
# the AWS IoT library.
zephyr_include_directories_ifdef(CONFIG_AWS_IOT_PROVISION_CERTIFICATES certs)
