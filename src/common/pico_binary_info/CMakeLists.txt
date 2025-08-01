add_library(pico_binary_info_headers INTERFACE)

target_include_directories(pico_binary_info_headers SYSTEM INTERFACE ${CMAKE_CURRENT_LIST_DIR}/include)

add_library(pico_binary_info INTERFACE)
if (COMMAND pico_add_platform_library)
    pico_add_platform_library(pico_binary_info)
endif()

target_link_libraries(pico_binary_info INTERFACE pico_binary_info_headers)

# pico_set_program_name(TARGET name)
# \brief\ Set the program name for the target
#
# \param\ name The program name to set
function(pico_set_program_name TARGET name)
    # PICO_BUILD_DEFINE: PICO_PROGRAM_NAME, value passed to pico_set_program_name, type=string, group=pico_binary_info
    target_compile_definitions(${TARGET} PRIVATE -DPICO_PROGRAM_NAME="${name}")
endfunction()

# pico_set_program_description(TARGET description)
# \brief\ Set the program description for the target
#
# \param\ description The program description to set
function(pico_set_program_description TARGET description)
    # since this is the command line, we will remove newlines
    string(REPLACE "\n" " " description ${description})
    string(REPLACE "\"" "\\\"" description ${description})
    # PICO_BUILD_DEFINE: PICO_PROGRAM_DESCRIPTION, value passed to pico_set_program_description, type=string, group=pico_binary_info
    target_compile_definitions(${TARGET} PRIVATE -DPICO_PROGRAM_DESCRIPTION="${description}")
endfunction()

# pico_set_program_url(TARGET url)
# \brief\ Set the program URL for the target
#
# \param\ url The program URL to set
function(pico_set_program_url TARGET url)
    # PICO_BUILD_DEFINE: PICO_PROGRAM_URL, value passed to pico_set_program_url, type=string, group=pico_binary_info
    target_compile_definitions(${TARGET} PRIVATE -DPICO_PROGRAM_URL="${url}")
endfunction()

# pico_set_program_version(TARGET version)
# \brief\ Set the program version for the target
#
# \param\ version The program version to set
function(pico_set_program_version TARGET version)
    # PICO_BUILD_DEFINE: PICO_PROGRAM_VERSION_STRING, value passed to pico_set_program_version, type=string, group=pico_binary_info
    target_compile_definitions(${TARGET} PRIVATE -DPICO_PROGRAM_VERSION_STRING="${version}")
endfunction()
