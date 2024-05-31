
cmake_minimum_required(VERSION 2.8...3.5)

# set(CMAKE_BUILD_TYPE "MinSizeRel" CACHE STRING "Choose the type of build, options are: Debug, Release, or MinSizeRel." FORCE)
set(CMAKE_C_FLAGS "-Wall -Wextra -pedantic -Werror -O2 -fPIC -DHAVE_VSNPRINTF -DHAVE_VSSCANF")

# pdcurses .c add
file(GLOB pdcurses_src "${PROJECT_SOURCE_DIR}/pdcurses/*.c")

# deps .c add
set(pdc_vt_src_files 
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcclip.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcdisp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcgetsc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdckbd.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcscrn.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcsetsc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcutil.c)

# vt library
add_library(pdcvt STATIC ${pdc_vt_src_files} ${pdcurses_src})
target_link_libraries(pdcvt)
target_include_directories(pdcvt    PUBLIC ${PROJECT_SOURCE_DIR}
                                    PRIVATE ${PROJECT_SOURCE_DIR}/common ${CMAKE_CURRENT_SOURCE_DIR})

# test demos
add_executable(vt_calendar ${PROJECT_SOURCE_DIR}/demos/calendar.c)
target_link_libraries(vt_calendar pdcvt)

add_executable(vt_init_col ${PROJECT_SOURCE_DIR}/demos/init_col.c)
target_link_libraries(vt_init_col pdcvt)

add_executable(vt_firework ${PROJECT_SOURCE_DIR}/demos/firework.c)
target_link_libraries(vt_firework pdcvt)

add_executable(vt_mbrot ${PROJECT_SOURCE_DIR}/demos/mbrot.c)
target_link_libraries(vt_mbrot pdcvt)

add_executable(vt_ozdemo ${PROJECT_SOURCE_DIR}/demos/ozdemo.c)
target_link_libraries(vt_ozdemo pdcvt)

add_executable(vt_newtest ${PROJECT_SOURCE_DIR}/demos/newtest.c)
target_link_libraries(vt_newtest pdcvt)

add_executable(vt_picsview ${PROJECT_SOURCE_DIR}/demos/picsview.c)
target_link_libraries(vt_picsview pdcvt)

add_executable(vt_ptest ${PROJECT_SOURCE_DIR}/demos/ptest.c)
target_link_libraries(vt_ptest pdcvt)

add_executable(vt_speed ${PROJECT_SOURCE_DIR}/demos/speed.c)
target_link_libraries(vt_speed pdcvt)

add_executable(vt_rain ${PROJECT_SOURCE_DIR}/demos/rain.c)
target_link_libraries(vt_rain pdcvt)

add_executable(vt_test_pan ${PROJECT_SOURCE_DIR}/demos/test_pan.c)
target_link_libraries(vt_test_pan pdcvt)

add_executable(vt_widetest ${PROJECT_SOURCE_DIR}/demos/widetest.c)
target_link_libraries(vt_widetest pdcvt)

add_executable(vt_testcurs ${PROJECT_SOURCE_DIR}/demos/testcurs.c)
target_link_libraries(vt_testcurs pdcvt)

add_executable(vt_tuidemo ${PROJECT_SOURCE_DIR}/demos/tuidemo.c ${PROJECT_SOURCE_DIR}/demos/tui.c)
target_link_libraries(vt_tuidemo pdcvt)

add_executable(vt_worm ${PROJECT_SOURCE_DIR}/demos/worm.c)
target_link_libraries(vt_worm pdcvt)

add_executable(vt_xmas ${PROJECT_SOURCE_DIR}/demos/xmas.c)
target_link_libraries(vt_xmas pdcvt)

