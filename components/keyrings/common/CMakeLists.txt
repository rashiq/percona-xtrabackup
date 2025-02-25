# Copyright (c) 2021, Oracle and/or its affiliates.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License, version 2.0,
# as published by the Free Software Foundation.
#
# This program is also distributed with certain software (including
# but not limited to OpenSSL) that is licensed under separate terms,
# as designated in a particular file or component or in included license
# documentation.  The authors of MySQL hereby grant you an additional
# permission to link the program and your derivative works with the
# separately licensed software that they have included with MySQL.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License, version 2.0, for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301  USA

ADD_WSHADOW_WARNING()

SET(KEYRING_COMMON_SOURCES
  # Component implementation helpers
  component_helpers/src/keyring_log_builtins_definition.cc
  # Config file reader
  # Data representation
  data/data.cc
  data/meta.cc
  data/psi_memory_resource.cpp
  # File reader/writer
  data_file/reader.cc
  data_file/writer.cc
  # Encryption
  encryption/aes.cc
  # JSON reader/writer
  json_data/json_reader.cc
  json_data/json_writer.cc
  # Utilities
  utils/utils.cc
  )

SET (KEYRING_COMMON_DEPENDENCIES
  GenError
  )

IF(COMPONENT_COMPILE_VISIBILITY)
  SET(COMPILE_OPTIONS_ARG COMPILE_OPTIONS "${COMPONENT_COMPILE_VISIBILITY}")
ENDIF()

INCLUDE_DIRECTORIES(SYSTEM
        ${BOOST_PATCHES_DIR}
        ${BOOST_INCLUDE_DIR})

ADD_CONVENIENCE_LIBRARY(
  keyring_common
  ${KEYRING_COMMON_SOURCES}
  ${COMPILE_OPTIONS_ARG}
  DEPENDENCIES ${KEYRING_COMMON_DEPENDENCIES}
  LINK_LIBRARIES library_mysys
)
TARGET_COMPILE_OPTIONS(keyring_common PUBLIC "-Wno-cast-qual")

