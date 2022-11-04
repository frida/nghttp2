config = configuration_data()
config.set('PACKAGE_VERSION', version)
config.set('PACKAGE_VERSION_NUM', version_num)

nghttp2ver_h = configure_file(
  input: 'nghttp2ver.h.in',
  output: 'nghttp2ver.h',
  configuration: config,
)

install_headers('nghttp2.h', nghttp2ver_h, subdir: 'nghttp2')
