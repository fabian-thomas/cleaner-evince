deps = backends_deps + [
  cairo_pdf_dep,
  cairo_ps_dep,
  libxml_dep,
  poppler_glib_dep,
]

shared_module(
  backend_name,
  sources: 'ev-poppler.c',
  include_directories: backends_incs,
  dependencies: deps,
  c_args: backends_cflags,
  gnu_symbol_visibility: 'hidden',
  install: true,
  install_dir: ev_backendsdir,
  name_suffix: name_suffix,
)
