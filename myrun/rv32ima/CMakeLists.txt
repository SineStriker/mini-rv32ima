project(rv32ima LANGUAGES C)

add_executable(${PROJECT_NAME} mini-rv32ima.h mini-rv32ima.c default64mbdtc.h)

get_filename_component(_include_dir ${MYRUN_HEADER_FILE} DIRECTORY)

target_include_directories(${PROJECT_NAME} PRIVATE ${_include_dir})

# Generate temporary header to prevent static error
file(GENERATE OUTPUT ${MYRUN_HEADER_FILE} CONTENT "const char binary_data[] = \"1\";")

add_custom_target(generate_header DEPENDS bintoh++)

# Generate real header after build generator
add_custom_command(TARGET generate_header
    COMMAND $<TARGET_FILE:bintoh++>
    ARGS ${MYRUN_EMBED_FILE} ${MYRUN_HEADER_FILE}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

# Force the rv32ima to build after generation
add_dependencies(${PROJECT_NAME} generate_header)

# Add a target to start the rv32ima
add_custom_target(myrun
    COMMAND $<TARGET_FILE:${PROJECT_NAME}> ${MYRUN_ARGUMENTS}
    WORKING_DIRECTORY $<TARGET_FILE_DIR:${PROJECT_NAME}>
)