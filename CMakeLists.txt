cmake_minimum_required(VERSION 3.10)
project(swipl-json)

include("../cmake/PrologPackage.cmake")
has_package(http HAVE_HTTP_PACKAGE)

set(JSON_PL_FILES json.pl json_convert.pl json_grammar.pl json_schema.pl)
set(JSON_COMPAT_FILES json.pl json_convert.pl js_grammar.pl)
prepend(JSON_COMPAT_FILES compat ${JSON_COMPAT_FILES})

swipl_plugin(
    json
    C_SOURCES json.c
    PL_LIBS ${JSON_PL_FILES})

test_libs(json json_schema)

if(HAVE_HTTP_PACKAGE)
set(JSON_HTTP_FILES)
if(NOT EMSCRIPTEN)
  set(JSON_HTTP_FILES http_json.pl)
endif()

  swipl_plugin(
      json_http_plugin
      PL_LIB_SUBDIR http
      PL_LIBS ${JSON_HTTP_FILES} ${JSON_COMPAT_FILES})
  add_dependencies(json json_http_plugin)
endif()

pkg_doc(json
	SOURCES
	    jsonmd.md)
