
set(SOURCE_FILES main.cpp Calculator.cpp graph.cpp graphing.cpp Keypad.cpp MCP23017.cpp Settings.cpp tabs.cpp easywsclient.cpp base64.cpp)

add_executable(${PROJECT_NAME} ${SOURCE_FILES})
set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/build/out")
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/lv_drivers ${CMAKE_SOURCE_DIR}/lvgl ${CMAKE_SOURCE_DIR}/schemas/include_gen ${CMAKE_SOURCE_DIR} include)
target_link_libraries(${PROJECT_NAME} lv_drivers lvgl nlohmann_json::nlohmann_json nlohmann_json_schema_validator)
if(LINUX_ENABLE)
    target_link_libraries(${PROJECT_NAME} ${libm} ${libpthread} ${libsdl2} ${libgiac} ${libgmp})
endif()
if(PI_ENABLE)
    target_link_libraries(${PROJECT_NAME} ${libm} ${libpthread} ${libgiac} ${libgmp} ${libi2c} ${libwiringPi})
endif()
