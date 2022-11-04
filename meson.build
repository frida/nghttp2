project('nghttp2', 'c', version: '1.51.0')

lt_cur = 38
lt_rev = 0
lt_age = 24

version = meson.project_version()
version_num = run_command(
  'python3', '-c', f'''
major, minor, patch = [int(digit) for digit in '@version@'.split('.')]
print("0x{:02x}{:02x}{:02x}".format(major, minor, patch))''',
  check: true,
).stdout().strip()

if host_machine.system() in ['hpux', 'netbsd', 'openbsd', 'sunos']
  library_version = '@0@.@1@'.format(lt_cur, lt_rev)
elif host_machine.system() == 'qnx'
  library_version = lt_cur.to_string()
else
  library_version = '@0@.@1@.@2@'.format(lt_cur - lt_age, lt_age, lt_rev)
endif

cc = meson.get_compiler('c')

cdata = configuration_data()

system_headers = [
  'arpa/inet.h',
  'netinet/in.h',
]
foreach h : system_headers
  if cc.check_header(h)
    cdata.set('HAVE_' + h.underscorify().to_upper(), 1)
  endif
endforeach

configure_file(
  configuration: cdata,
  output: 'config.h'
)
add_project_arguments('-DHAVE_CONFIG_H', language: 'c')

incdirs = include_directories(
  '.',
  'lib' / 'includes',
)

subdir('lib')
