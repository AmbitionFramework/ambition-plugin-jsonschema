SET( APJS_VALA_FILES
	JSONSchemaPlugin.vala
)

vala_precompile(APJS_VALA_C
	${APJS_VALA_FILES}
PACKAGES
	${APJS_VALA_PACKAGES}
OPTIONS
	${DEFAULT_VALA_OPTIONS}
GENERATE_VAPI
	${PPKGNAME}-${PPKGVERSION}
GENERATE_HEADER
	${PPKGNAME}-${PPKGVERSION})

link_directories(${APJS_LIB_PATHS})
add_definitions(${APJS_DEPS_CFLAGS_ALL})

add_library(${PPKGNAME}-${PPKGVERSION} SHARED ${APJS_VALA_C})
target_link_libraries(${PPKGNAME}-${PPKGVERSION} ${APJS_DEPS_LIBRARIES})

install (
	FILES
		${CMAKE_CURRENT_BINARY_DIR}/${PPKGNAME}-${PPKGVERSION}.vapi
		${PPKGNAME}-${PPKGVERSION}.deps
		${CMAKE_CURRENT_BINARY_DIR}/${PPKGNAME}-${PPKGVERSION}.h
	DESTINATION ${CMAKE_INSTALL_PREFIX}
)
install (
	TARGETS ${PPKGNAME}-${PPKGVERSION}
	DESTINATION ${CMAKE_INSTALL_PREFIX}
)
