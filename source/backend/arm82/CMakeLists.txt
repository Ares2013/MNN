if(MNN_ARM82)
  if(CMAKE_SYSTEM_PROCESSOR MATCHES "^aarch64" OR IOS_ARCH STREQUAL "arm64")
    file(GLOB MNN_ARM82_SRCS "${CMAKE_CURRENT_LIST_DIR}/*.cpp")
    file(GLOB MNN_ARM82_SRCS_ASM "${CMAKE_CURRENT_LIST_DIR}/asm/arm64/*")
    add_definitions(-march=armv8.2a+fp16)
    add_library(
        MNNARM82
        OBJECT
        ${MNN_ARM82_SRCS}
        ${MNN_ARM82_SRCS_ASM}
    )
    target_include_directories(MNNARM82 PRIVATE ${CMAKE_CURRENT_LIST_DIR}/asm/)
    list(APPEND MNN_OBJECTS_TO_LINK $<TARGET_OBJECTS:MNNARM82>)
    list(APPEND MNN_TARGETS MNNARM82)
    SET(MNN_OBJECTS_TO_LINK "${MNN_OBJECTS_TO_LINK}" PARENT_SCOPE)
    SET(MNN_TARGETS "${MNN_TARGETS}" PARENT_SCOPE)
  endif()
endif()
