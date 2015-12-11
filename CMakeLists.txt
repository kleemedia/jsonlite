cmake_minimum_required(VERSION 3.4 FATAL_ERROR)

set(SRC_DIR jsonlite/src)
set(HEADER_DIR jsonlite/include)

set(SOURCE
	${SRC_DIR}/jsonlite.c
	${SRC_DIR}/jsonlite_buffer.c
	${SRC_DIR}/jsonlite_builder.c
	${SRC_DIR}/jsonlite_parser.c
	${SRC_DIR}/jsonlite_stream.c
	${SRC_DIR}/jsonlite_token.c
	${SRC_DIR}/jsonlite_token_pool.c
)

set(HEADER
	${HEADER_DIR}/jsonlite.h
	${HEADER_DIR}/jsonlite_buffer.h
	${HEADER_DIR}/jsonlite_builder.h
	${HEADER_DIR}/jsonlite_parser.h
	${HEADER_DIR}/jsonlite_stream.h
	${HEADER_DIR}/jsonlite_token.h
	${HEADER_DIR}/jsonlite_token_pool.h
	${HEADER_DIR}/jsonlite_types.h
)

add_library(jsonlite STATIC
	${SOURCE}
)

target_include_directories(jsonlite PUBLIC ${HEADER_DIR})

IF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    # Linux specific code
    target_compile_options(jsonlite PUBLIC -fPIC)
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

install(FILES
    ${HEADER}
	DESTINATION ${CMAKE_BINARY_DIR}/include
)

