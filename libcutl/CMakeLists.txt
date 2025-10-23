set(headers_ixx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/cxx-indenter.ixx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-id.ixx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-info.ixx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/path.ixx
 ${CMAKE_CURRENT_SOURCE_DIR}/shared-ptr/base.ixx
)

set(headers
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/code-stream.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/code-stream.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/context.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/context.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/cxx-indenter.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/cxx-indenter.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/sloc-counter.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/sloc-counter.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/traversal.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/traversal.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-id.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-id.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-info.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/any.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/graph.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/graph.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/key.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/map-iterator.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/multi-index.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/container/pointer-iterator.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/auto-remove.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/exception.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/path.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/path.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/answer.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/class-p.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/polymorphic-p.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/remove-c.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/remove-cv.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/remove-p.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/meta/remove-v.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/re/re.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/shared-ptr/base.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/shared-ptr/base.txx
 ${CMAKE_CURRENT_SOURCE_DIR}/exception.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/export.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/re.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/shared-ptr.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/static-ptr.hxx
 ${CMAKE_CURRENT_SOURCE_DIR}/version.hxx
)

set(sources
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/context.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/cxx-indenter.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/compiler/type-info.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/auto-remove.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/exception.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/fs/path.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/re/re.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/shared-ptr/base.cxx
 ${CMAKE_CURRENT_SOURCE_DIR}/exception.cxx
)

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${headers} ${headers_ixx} ${sources})

add_library(cutl)

target_sources(cutl
 PRIVATE
 ${sources}
 ${headers_ixx} # Workaround to prevent Visual Studio to compile these files
 PUBLIC
 ${headers}
)

set_source_files_properties(${headers_ixx} PROPERTIES HEADER_FILE_ONLY TRUE)

if(BUILD_SHARED_LIBS)
 target_compile_definitions(cutl
 PRIVATE LIBCUTL_SHARED_BUILD
 INTERFACE LIBCUTL_SHARED
 )
else()
 target_compile_definitions(cutl
 PRIVATE LIBCUTL_STATIC_BUILD
 INTERFACE LIBCUTL_STATIC
 )
endif()

target_include_directories(cutl
 PUBLIC
 $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/..>
 $<INSTALL_INTERFACE:include>
)
