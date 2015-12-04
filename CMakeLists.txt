cmake_minimum_required (VERSION 2.6)
project (decnumber)

include(TestBigEndian)
TEST_BIG_ENDIAN(BIG_ENDIAN)

if(BIGENDIAN)
  add_definitions(-DDECLITEND=0)
endif(BIGENDIAN)

set(decnumber_VERSION 3.68)
set(decnumber_SOVERSION 3)

set(decnumber_SOURCES
    decContext.c
    decDouble.c
    decNumber.c
    decPacked.c
    decQuad.c
    decSingle.c
    decimal128.c
    decimal32.c
    decimal64.c)

set(decnumber_HEADERS
    decContext.h
    decDouble.h
    decDPD.h
    decNumber.h
    decPacked.h
    decQuad.h
    decSingle.h
    decimal128.h
    decimal32.h
    decimal64.h
)

add_library(decnumber_shared SHARED ${decnumber_SOURCES})
add_library(decnumber_static STATIC ${decnumber_SOURCES})

install(TARGETS decnumber_shared
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin
        COMPONENT libraries)

set_target_properties(decnumber_shared
  PROPERTIES
    VERSION
      ${decnumber_VERSION}
    SOVERSION
      ${decnumber_SOVERSION}
    OUTPUT_NAME
      decnumber
    MACOSX_RPATH
      ON)

install(TARGETS decnumber_static
        ARCHIVE DESTINATION lib
        COMPONENT libraries)

set_target_properties(decnumber_static
  PROPERTIES
    VERSION
      ${decnumber_VERSION}
    SOVERSION
      ${decnumber_SOVERSION}
    OUTPUT_NAME
      decnumber)

install(FILES ${decnumber_HEADERS}
        DESTINATION include/${PROJECT_NAME}
        COMPONENT headers)
