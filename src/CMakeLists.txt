include(GNUInstallDirs)
include(GenerateExportHeader)

add_executable(SKEL_EXECUTABLE)
target_sources(SKEL_EXECUTABLE PRIVATE main.cpp)
target_link_libraries(SKEL_EXECUTABLE PRIVATE project_options project_warnings spdlog::spdlog)
target_include_directories(SKEL_EXECUTABLE PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
define_file_basename_for_sources(SKEL_EXECUTABLE)

# add this only for libraries
# generate_export_header(SKEL_EXECUTABLE)

set_target_properties(SKEL_EXECUTABLE PROPERTIES SOVERSION 1 VERSION 1.0.0)
target_compile_definitions(SKEL_EXECUTABLE PRIVATE PZ_ENABLE_ASSERTS)

##install stuff
install(TARGETS SKEL_EXECUTABLE spdlog fmt project_options project_warnings EXPORT SKEL_EXECUTABLEConfig)
install(EXPORT SKEL_EXECUTABLEConfig DESTINATION  ${CMAKE_INSTALL_LIBDIR}/cmake) 


configure_file(version.h.in version.h @ONLY)
