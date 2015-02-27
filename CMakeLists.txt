project(xtract)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")

file(GLOB HEADER_FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/c-ringbuf/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/dywapitchtrack/*.h")
file(GLOB SOURCE_FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/c-ringbuf/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/dywapitchtrack/*.c")

if(ANDROID)
    list(APPEND HEADER_FILES
         "${CMAKE_CURRENT_SOURCE_DIR}/src/ooura/fftsg.h")
    list(APPEND SOURCE_FILES
         "${CMAKE_CURRENT_SOURCE_DIR}/src/ooura/fftsg.c")

    add_definitions(-DUSE_OOURA)
elseif(PR_IOS_BUILD)
    set(LIBRARIES "-framework Accelerate")
endif()

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")

add_library(xtract STATIC ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(xtract ${LIBRARIES})
