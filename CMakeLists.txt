cmake_minimum_required(VERSION 3.6)
project(arrow)

add_definitions(-DARROW_EXPORTING)
add_definitions(-DARROW_USE_SIMD)
add_definitions(-DRAPIDJSON_SSE42)
add_definitions(-D _HAS_CXX17=1)
add_definitions(-D _HAS_CXX20=1)
add_definitions(-D _WIN32_WINNT=0x0601)
add_definitions(-D _MSC_VER=1920)
set(CMAKE_CONFIGURATION_TYPES "Debug" CACHE STRING "" FORCE)

include_directories(src)
include_directories(ext/include)
include_directories(src/arrow/io)

set(ARROW_SRCS
    src/arrow/array.cc
    src/arrow/builder.cc
    src/arrow/array/builder_adaptive.cc
    src/arrow/array/builder_base.cc
    src/arrow/array/builder_binary.cc
    src/arrow/array/builder_decimal.cc
    src/arrow/array/builder_dict.cc
    src/arrow/array/builder_nested.cc
    src/arrow/array/builder_primitive.cc
    src/arrow/array/builder_union.cc
    src/arrow/buffer.cc
    src/arrow/compare.cc
    src/arrow/extension_type.cc
    src/arrow/memory_pool.cc
    src/arrow/pretty_print.cc
    src/arrow/record_batch.cc
    src/arrow/scalar.cc
    src/arrow/sparse_tensor.cc
    src/arrow/status.cc
    src/arrow/table.cc
    src/arrow/table_builder.cc
    src/arrow/tensor.cc
    src/arrow/type.cc
    src/arrow/visitor.cc
    src/arrow/csv/converter.cc
    src/arrow/csv/chunker.cc
    src/arrow/csv/column-builder.cc
    src/arrow/csv/options.cc
    src/arrow/csv/parser.cc
    src/arrow/csv/reader.cc
    src/arrow/json/options.cc
    src/arrow/json/chunker.cc
    src/arrow/json/parser.cc
    src/arrow/json/reader.cc
    src/arrow/io/buffered.cc
    src/arrow/io/compressed.cc
    src/arrow/io/file.cc
    src/arrow/io/interfaces.cc
    src/arrow/io/memory.cc
    src/arrow/io/readahead.cc
    src/arrow/testing/util.cc
    src/arrow/util/basic_decimal.cc
    src/arrow/util/bit-util.cc
    src/arrow/util/concatenate.cc
    src/arrow/util/compression.cc
    src/arrow/util/cpu-info.cc
    src/arrow/util/decimal.cc
    src/arrow/util/int-util.cc
    src/arrow/util/io-util.cc
    src/arrow/util/logging.cc
    src/arrow/util/key_value_metadata.cc
    src/arrow/util/memory.cc
    src/arrow/util/task-group.cc
    src/arrow/util/thread-pool.cc
    src/arrow/util/trie.cc
    src/arrow/util/uri.cc
    src/arrow/util/utf8.cc
    src/arrow/vendored/datetime/tz.cpp)

# set(PARQUET_SRCS
#     src/parquet/arrow/reader.cc
#     src/parquet/arrow/record_reader.cc
#     src/parquet/arrow/schema.cc
#     src/parquet/arrow/writer.cc
#     src/parquet/bloom_filter.cc
#     src/parquet/column_reader.cc
#     src/parquet/column_scanner.cc
#     src/parquet/column_writer.cc
#     src/parquet/encoding.cc
#     src/parquet/file_reader.cc
#     src/parquet/file_writer.cc
#     src/parquet/metadata.cc
#     src/parquet/murmur3.cc
#     src/parquet/printer.cc
#     src/parquet/schema.cc
#     src/parquet/statistics.cc
#     src/parquet/types.cc
#     src/parquet/util/comparison.cc
#     src/parquet/util/memory.cc)
#   src/parquet/parquet_constants.cpp
#   src/parquet/parquet_types.cpp
# add_library(arrow STATIC ${ARROW_SRCS} ${PARQUET_SRCS})


add_library(arrow STATIC ${ARROW_SRCS})
target_compile_features(arrow PRIVATE cxx_std_17)
target_compile_options(arrow PRIVATE /bigobj)
target_include_directories(arrow PRIVATE ext/include)
target_link_libraries(arrow ext/lib/gtestd)
