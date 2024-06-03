cmake_minimum_required(VERSION 2.8...3.5)

set(CMAKE_C_FLAGS "-nologo -c -Ox -W4 -D_CRT_SECURE_NO_WARNINGS  -DPDC_DLL_BUILD")
# wingui # -nologo -c -Ox -MT -W4 -D_CRT_SECURE_NO_WARNINGS  -DPDC_DLL_BUILD  -DPDC_FORCE_UTF8
# wincon # -nologo -c -Ox -W4 -D_CRT_SECURE_NO_WARNINGS  -DPDC_DLL_BUILD
# vt # -nologo -c -O1 -W4 -D_CRT_SECURE_NO_WARNINGS -DCHTYPE_32 

# pdcurses .c add
file(GLOB pdcurses_src "${PROJECT_SOURCE_DIR}/pdcurses/*.c")

# deps .c add
set(pdc_wincon_src_files 
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcclip.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcdisp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcgetsc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdckbd.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcscrn.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcsetsc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pdcutil.c)

# vt library
add_library(pdcwincon STATIC ${pdc_vt_src_files} ${pdcurses_src})
target_link_libraries(pdcwincon)
target_include_directories(pdcwincon    PUBLIC ${PROJECT_SOURCE_DIR}
                                        PRIVATE ${PROJECT_SOURCE_DIR}/common ${CMAKE_CURRENT_SOURCE_DIR})

# test demos
add_executable(wincon_calendar ${PROJECT_SOURCE_DIR}/demos/calendar.c)
target_link_libraries(wincon_calendar pdcwincon)

add_executable(wincon_init_col ${PROJECT_SOURCE_DIR}/demos/init_col.c)
target_link_libraries(wincon_init_col pdcwincon)

add_executable(wincon_firework ${PROJECT_SOURCE_DIR}/demos/firework.c)
target_link_libraries(wincon_firework pdcwincon)

add_executable(wincon_mbrot ${PROJECT_SOURCE_DIR}/demos/mbrot.c)
target_link_libraries(wincon_mbrot pdcwincon)

add_executable(wincon_ozdemo ${PROJECT_SOURCE_DIR}/demos/ozdemo.c)
target_link_libraries(wincon_ozdemo pdcwincon)

add_executable(wincon_newtest ${PROJECT_SOURCE_DIR}/demos/newtest.c)
target_link_libraries(wincon_newtest pdcwincon)

add_executable(wincon_picsview ${PROJECT_SOURCE_DIR}/demos/picsview.c)
target_link_libraries(wincon_picsview pdcwincon)

add_executable(wincon_ptest ${PROJECT_SOURCE_DIR}/demos/ptest.c)
target_link_libraries(wincon_ptest pdcwincon)

add_executable(wincon_speed ${PROJECT_SOURCE_DIR}/demos/speed.c)
target_link_libraries(wincon_speed pdcwincon)

add_executable(wincon_rain ${PROJECT_SOURCE_DIR}/demos/rain.c)
target_link_libraries(wincon_rain pdcwincon)

add_executable(wincon_test_pan ${PROJECT_SOURCE_DIR}/demos/test_pan.c)
target_link_libraries(wincon_test_pan pdcwincon)

add_executable(wincon_widetest ${PROJECT_SOURCE_DIR}/demos/widetest.c)
target_link_libraries(wincon_widetest pdcwincon)

add_executable(wincon_testcurs ${PROJECT_SOURCE_DIR}/demos/testcurs.c)
target_link_libraries(wincon_testcurs pdcwincon)

add_executable(wincon_tuidemo ${PROJECT_SOURCE_DIR}/demos/tuidemo.c ${PROJECT_SOURCE_DIR}/demos/tui.c)
target_link_libraries(wincon_tuidemo pdcwincon)

add_executable(wincon_worm ${PROJECT_SOURCE_DIR}/demos/worm.c)
target_link_libraries(wincon_worm pdcwincon)

add_executable(wincon_xmas ${PROJECT_SOURCE_DIR}/demos/xmas.c)
target_link_libraries(wincon_xmas pdcwincon)
