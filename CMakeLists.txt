cmake_minimum_required(VERSION 3.7.2)
project(topk_words CXX)

set(CMAKE_CXX_STANDARD 17)

add_executable(topk_words topk_words.cpp)

# clang-format
find_program(CLANG-FORMAT_PATH NAMES clang-format REQUIRED)
message(STATUS "Найден clang-format: ${CLANG-FORMAT_PATH}")
file(GLOB_RECURSE CLANG-FORMAT_SRC CONFIGURE_DEPENDS *.*pp)
message(STATUS "Найдены src: ${CLANG-FORMAT_SRC}")
add_custom_target(clangformat
    COMMAND ${CLANG-FORMAT_PATH} -i ${CLANG-FORMAT_SRC}
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
    COMMENT "Форматирование ${PROJECT_NAME} с ${CLANG-FORMAT_PATH}"
)
add_dependencies(topk_words clangformat)

if (MSVC)
    target_compile_options(topk_words PUBLIC /W4)
else ()
    target_compile_options(topk_words PUBLIC -Wall -Wextra -Wpedantic 
#    		-Wconversion 
#    		-Wsign-conversion
    		)
endif ()
