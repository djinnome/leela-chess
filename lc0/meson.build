project('lc0', 'cpp', 
        default_options : ['c_std=c17', 'cpp_std=c++17'])

# add_global_arguments('-Wno-macro-redefined', language : 'cpp')
cc = meson.get_compiler('cpp')

# Installed from https://github.com/FloopCZ/tensorflow_cc
tensorflow_cc = declare_dependency(
  include_directories: include_directories(
    '/usr/local/include/tensorflow',
    '/usr/local/include/tensorflow/bazel-genfiles',
    '/usr/local/include/tensorflow/tensorflow/contrib/makefile/downloads',
    '/usr/local/include/tensorflow/tensorflow/contrib/makefile/downloads/eigen',
    '/usr/local/include/tensorflow/tensorflow/contrib/makefile/downloads/gemmlowp',
    '/usr/local/include/tensorflow/tensorflow/contrib/makefile/downloads/nsync/public',
    '/usr/local/include/tensorflow/tensorflow/contrib/makefile/gen/protobuf-host/include',
  ),
  dependencies: [
      cc.find_library('libtensorflow_cc', dirs: '/usr/local/lib/tensorflow_cc/'),
      cc.find_library('dl'),
      cc.find_library('pthread'),
      cc.find_library('libprotobuf', dirs: '/usr/local/lib/tensorflow_cc/'),
  ],
)

deps = []
deps += tensorflow_cc
deps += cc.find_library('stdc++fs')
# deps += dependency('libprofiler')

files = [
  'src/chess/bitboard.cc',
  'src/chess/board.cc',
  'src/neural/loader.cc',
  'src/neural/network_tf.cc',
  'src/mcts/search.cc',
  'src/mcts/node.cc',
  'src/engine.cc',
  'src/uciloop.cc',
  'src/ucioptions.cc',
  'src/utils/transpose.cc',
]

includes = []
includes += include_directories('src')

executable('lc0', 'src/main.cc',
  files, include_directories: includes, dependencies: deps)


### Tests

test_deps = deps
test_deps += dependency('gtest')

test('ChessBoard',
  executable('chessboard_test', 'src/chess/board_test.cc',
  files, include_directories: includes, dependencies: test_deps
))

test('Network',
  executable('network_test', 'src/neural/network_test.cc',
  files, include_directories: includes, dependencies: test_deps
))
