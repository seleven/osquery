# Copyright (c) 2014-present, Facebook, Inc.
# All rights reserved.
#
# This source code is licensed in accordance with the terms specified in
# the LICENSE file found in the root directory of this source tree.

function(osqueryUtilsAzureMain)
  generateOsqueryUtilsAzure()
endfunction()

function(generateOsqueryUtilsAzure)
  add_osquery_library(osquery_utils_azure EXCLUDE_FROM_ALL
    azure_util.cpp
  )

  target_link_libraries(osquery_utils_azure PUBLIC
    osquery_cxx_settings
    osquery_remote_httpclient
    osquery_remote_transports_transportstls
    osquery_utils_json
    osquery_utils_status
  )

  set(public_header_files
    azure_util.h
  )

  generateIncludeNamespace(osquery_utils_azure "osquery/utils/azure" "FILE_ONLY" ${public_header_files})

  add_test(NAME osquery_utils_aws_tests-test COMMAND osquery_utils_aws_tests-test)

  set_tests_properties(
    osquery_utils_aws_tests-test
    PROPERTIES ENVIRONMENT "TEST_CONF_FILES_DIR=${TEST_CONFIGS_DIR}"
  )
endfunction()

osqueryUtilsAzureMain()
