project('ads', 'cpp')

qt5_mod = import('qt5')
qt5_dep = dependency('qt5', modules: ['Core', 'Gui', 'Widgets'])

moc_headers = [
    'src/ads_globals.h',
    'src/DockAreaTabBar.h',
    'src/DockAreaTitleBar.h',
    'src/DockAreaWidget.h',
    'src/DockContainerWidget.h',
    'src/DockManager.h',
    'src/DockOverlay.h',
    'src/DockSplitter.h',
    'src/DockWidget.h',
    'src/DockWidgetTab.h',
	'src/DockingStateReader.h',
    'src/ElidingLabel.h',
    'src/FloatingDockContainer.h',
	'src/FloatingDragPreview.h',
	'src/IconProvider.h',
	'src/DockComponentsFactory.h',
    'src/DockFocusController.h',
    'src/DockAreaTitleBar_p.h'
]

src = [
    'src/ads_globals.cpp',
    'src/DockAreaTabBar.cpp',
    'src/DockAreaTitleBar.cpp',
    'src/DockAreaWidget.cpp',
    'src/DockContainerWidget.cpp',
    'src/DockManager.cpp',
    'src/DockOverlay.cpp',
    'src/DockSplitter.cpp',
    'src/DockWidget.cpp',
    'src/DockWidgetTab.cpp',
	'src/DockingStateReader.cpp',
    'src/ElidingLabel.cpp',
    'src/FloatingDockContainer.cpp',
	'src/FloatingDragPreview.cpp',
	'src/IconProvider.cpp',
	'src/DockComponentsFactory.cpp',
    'src/DockFocusController.cpp',
]

if target_machine.system() == 'linux'
    extra_deps += dependency('qt5', modules: ['X11Extras'])
    extra_deps += dependency('xcb')
    src += 'src/linux/FloatingWidgetTitleBar.cpp'
endif

rc_files = 'src/ads.qrc'

processed = qt5_mod.preprocess(
  qresources : rc_files,
  moc_headers : moc_headers,
)

moc = find_program('moc')

processed2 = custom_target('custom_moc',
  input : ['src/DockAreaTitleBar.cpp'],
  output : ['DockAreaTitleBar.moc'],
  command : [moc, '@INPUT@', '-o', '@OUTPUT@'],
)

defs = ['-DADS_SHARED_EXPORT', '-DQT_NO_DEBUG_OUTPUT']

ads_lib = shared_library('ads',
  name_prefix: 'lib',
  sources : src + processed + [processed2],
  cpp_args: defs,
  include_directories : include_directories('src'),
  dependencies : [qt5_dep] + extra_deps,
)

ads_dep = declare_dependency(
  link_with : ads_lib,
  include_directories : include_directories('.', 'src', is_system : true),
)

