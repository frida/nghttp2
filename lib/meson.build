subdir('includes')

sources = [
  'nghttp2_pq.c',
  'nghttp2_map.c',
  'nghttp2_queue.c',
  'nghttp2_frame.c',
  'nghttp2_buf.c',
  'nghttp2_stream.c',
  'nghttp2_outbound_item.c',
  'nghttp2_session.c',
  'nghttp2_submit.c',
  'nghttp2_helper.c',
  'nghttp2_npn.c',
  'nghttp2_hd.c',
  'nghttp2_hd_huffman.c',
  'nghttp2_hd_huffman_data.c',
  'nghttp2_version.c',
  'nghttp2_priority_spec.c',
  'nghttp2_option.c',
  'nghttp2_callbacks.c',
  'nghttp2_mem.c',
  'nghttp2_http.c',
  'nghttp2_rcbuf.c',
  'nghttp2_extpri.c',
  'nghttp2_debug.c',
]

public_cflags = []
if get_option('default_library') == 'static'
  public_cflags += '-DNGHTTP2_STATICLIB'
endif

libnghttp2 = library('nghttp2', sources,
  version: library_version,
  c_args: ['-DBUILDING_NGHTTP2'] + public_cflags,
  include_directories: incdirs,
  install: true,
)

libnghttp2_dep = declare_dependency(
  include_directories: incdirs,
  compile_args: public_cflags,
  link_with: libnghttp2,
)

pkg = import('pkgconfig')
pkg.generate(libnghttp2,
  filebase: 'libnghttp2',
  description: 'HTTP/2 C library',
  url: 'https://github.com/nghttp2/nghttp2',
  extra_cflags: public_cflags,
)

meson.override_dependency('libnghttp2', libnghttp2_dep)
