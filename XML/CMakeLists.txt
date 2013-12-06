set(LIBNAME "PocoXML")

aux_source_directory(src SRCS)

add_definitions(-D_USRDLL -DXML_NS -DXML_DTD -DHAVE_EXPAT_CONFIG_H -DXML_EXPORTS)

add_library( ${LIBNAME} ${LIB_MODE} ${SRCS} )
target_link_libraries( ${LIBNAME} PocoFoundation)

install(
    DIRECTORY include/Poco
    DESTINATION include
    PATTERN ".svn" EXCLUDE
    )
    
install(
    TARGETS ${LIBNAME}
    DESTINATION lib
    )


