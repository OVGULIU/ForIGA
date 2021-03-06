project(BasisTests Fortran)

enable_language(Fortran)

file( GLOB ${PROJECT_NAME}_sources "bspline_test_fixture.f90" )

add_library( ${PROJECT_NAME} SHARED ${${PROJECT_NAME}_sources} )

install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib/shared)

target_link_libraries( ${PROJECT_NAME} util basis)

# file(GLOB pf_files "*.pf")

# set(testSuites ${PROJECT_BINARY_DIR}/generated/testSuites.inc)

# file(WRITE ${testSuites} "")
# message(STATUS "pfUnitDirectory:" ${PFUNIT_DIR})

# set(_test_sources)
# foreach(pf ${pf_files})
#     get_filename_component(_test ${pf} NAME_WE)
#     message(STATUS "Adding test ${_test}")
#     set(test_dependency ${PROJECT_SOURCE_DIR}/${_test}.pf)
#     add_custom_command(
#         OUTPUT ${PROJECT_BINARY_DIR}/generated/${_test}.F90
#         COMMAND python ${PFUNIT_DIR}/bin/pFUnitParser.py ${PROJECT_SOURCE_DIR}/${_test}.pf ${PROJECT_BINARY_DIR}/generated/${_test}.F90
#         DEPENDS ${test_dependency}
#         )
#     set(_test_sources ${_test_sources} ${PROJECT_BINARY_DIR}/generated/${_test}.F90 )
#     file(APPEND ${PROJECT_BINARY_DIR}/generated/testSuites.inc "ADD_TEST_SUITE(${_test}_suite)\n")
#     message(STATUS ${_test_sources})
# endforeach()

# set_source_files_properties(${PFUNIT_DIR}/include/driver.F90 PROPERTIES GENERATED 1)

# # pfunit -- especially without MPI, has some unused variables. We don't want to
# # bother the user with this.
# IF(${CMAKE_Fortran_COMPILER_ID} MATCHES "GNU")
#     string(REGEX REPLACE " -Wall" "" CMAKE_Fortran_FLAGS_DEBUG "${CMAKE_Fortran_FLAGS_DEBUG}")
# ELSEIF(${CMAKE_Fortran_COMPILER_ID} MATCHES "Intel")
#     set(CMAKE_Fortran_FLAGS_DEBUG "${CMAKE_Fortran_FLAGS_DEBUG} -diag-disable 7712")
# ENDIF(${CMAKE_Fortran_COMPILER_ID} MATCHES "GNU")


# include_directories(
#     ${PROJECT_SOURCE_DIR}
#     ${PROJECT_BINARY_DIR}/generated
#     ${PFUNIT_DIR}/include
#     ${PFUNIT_DIR}/mod
#     )

# add_executable(
#   ${PROJECT_NAME}
#   ${PFUNIT_DIR}/include/driver.F90
#   ${_test_sources}
# )

# target_link_libraries(
#   ${PROJECT_NAME}
#   ${PFUNIT_DIR}/lib/libpfunit.a
#   util
#   basis
# )
