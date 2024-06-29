# project setting
# -----------------------------------------------------------------
project(
  'shootingstr',
  'c',
  default_options : [
    'warning_level=3',
    'c_std=c23'
  ]
)
# -----------------------------------------------------------------

# yyjson install
# -----------------------------------------------------------------
cmake = import('cmake')
yyjson_options = cmake.subproject_options()
yyjson_options.add_cmake_defines({
  'CMAKE_C_COMPILER': 'gcc'
})

yyjson_subproject = cmake.subproject('yyjson', options: yyjson_options)
yyjson_dep = yyjson_subproject.dependency('yyjson')
# -----------------------------------------------------------------

# # openssl install
# # -----------------------------------------------------------------
# libopenssl_options = cmake.subproject_options()
# libopenssl_options.add_cmake_defines({
#   'BUILD_OPENSSL': 'ON',
#   'OPENSSL_ENABLE_TESTS': 'OFF',
#   'OPENSSL_BUILD_VERSION': '3.3.1',
#   'CMAKE_CXX_COMPILER': '/usr/bin/g++',
#   'CMAKE_C_COMPILER': '/usr/bin/gcc'
# })
# #libopenssl_subproject = cmake.subproject('openssl-cmake', options: libopenssl_options)
# libopenssl_subproject = cmake.subproject('openssl-cmake', options: libopenssl_options)
# libopenssl_dep = libopenssl_subproject.dependency('openssl-cmake')
# # -----------------------------------------------------------------

# libwebsockets install
# -----------------------------------------------------------------

libwebsockets_options = cmake.subproject_options()
libwebsockets_options.add_cmake_defines({
  'CMAKE_BUILD_TYPE': 'Release',
  'CMAKE_C_COMPILER': 'gcc',
  'LWS_WITH_SSL': 'ON',
  'LWS_WITHOUT_TESTAPPS': 'ON',
  'LWS_WITHOUT_TEST_SERVER': 'ON',
  'LWS_WITHOUT_TEST_CLIENT': 'ON',
  'LWS_WITH_NO_LOGS': 'ON',
  'LWS_OPENSSL_INCLUDE_DIRS': '/usr/include/openssl/',
  'LWS_OPENSSL_LIBRARIES': '/usr/lib/x86_64-linux-gnu/'
})

#'LWS_WITH_ZLIB': 'ON',
#  'CMAKE_C_FLAGS': 
#libwebsockets_subproject = cmake.subproject('libwebsockets', options: libwebsockets_options, dependencies: [libopenssl_dep])
libwebsockets_options.append_compile_args('c','-Wno-implicit-function-declaration', '-Wno-unused-parameter', '-Wno-pedantic')
libwebsockets_subproject = cmake.subproject(
  'libwebsockets',
  options: libwebsockets_options
)
libwebsockets_dep = libwebsockets_subproject.dependency('websockets', include_type: 'system')
libwebsockets = subproject('libwebsockets')
libwebsockets_dep = libwebsockets.get_variable('websockets_dep')
#libwebsockets_dep = dependency('libwebsockets')

sources = ['../src/main.c']

executable(
  'shootingstr',
  sources,
  link_args : [
    #'-no-as-needed',
    '-lssl',
    '-lcap'
  ],
  dependencies: [yyjson_dep, libwebsockets_dep],
  install: false
)
# -----------------------------------------------------------------
