subdir('mdvi-lib')

sources = files(
  'cairo-device.c',
  'dvi-document.c',
  'fonts.c',
  'texmfcnf.c',
)

deps = backends_deps + [
  libmdvi_dep,
  libspectre_dep,
  kpathsea_dep,
  m_dep
]

shared_module(
  backend_name,
  sources: sources,
  include_directories: backends_incs,
  dependencies: deps,
  c_args: backends_cflags,
  gnu_symbol_visibility: 'hidden',
  install: true,
  install_dir: ev_backendsdir,
  name_suffix: name_suffix,
)
