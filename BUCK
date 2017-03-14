def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

CONFIG_TYPES_H = """
#ifndef __CONFIG_TYPES_H__
#define __CONFIG_TYPES_H__

/* these are filled in by configure */
#define INCLUDE_INTTYPES_H 1
#define INCLUDE_STDINT_H 1
#define INCLUDE_SYS_TYPES_H 1

#if INCLUDE_INTTYPES_H
#  include <inttypes.h>
#endif
#if INCLUDE_STDINT_H
#  include <stdint.h>
#endif
#if INCLUDE_SYS_TYPES_H
#  include <sys/types.h>
#endif

typedef int16_t ogg_int16_t;
typedef uint16_t ogg_uint16_t;
typedef int32_t ogg_int32_t;
typedef uint32_t ogg_uint32_t;
typedef int64_t ogg_int64_t;

#endif
"""

genrule(
  name = 'config_types.h',
  out = 'config_types.h',
  cmd = 'echo "' + CONFIG_TYPES_H + '" > $OUT',
)

cxx_library(
  name = 'ogg',
  header_namespace = 'ogg',
  exported_headers = merge_dicts(subdir_glob([
    ('include/ogg', '*.h'),
  ]), {
    'config_types.h': ':config_types.h',
  }),
  srcs = glob([
    'src/*.c',
  ]),
  visibility = [
    'PUBLIC',
  ],
)
