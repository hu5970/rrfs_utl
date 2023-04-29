list(APPEND src_hrrr_fvcom
  kinds.f90 module_nwp.f90  module_nwp_base.f90  process_FVCOM.f90 )

add_executable(hrrr_fvcom.exe ${src_hrrr_fvcom})
target_link_libraries(hrrr_fvcom.exe PRIVATE 
                                          PRIVATE gsi::gsi
                                          PRIVATE ${PROJECT_NAME}::ncio
                                          PRIVATE NetCDF::NetCDF_Fortran
                                          PRIVATE MPI::MPI_Fortran)

if(OpenMP_Fortran_FOUND)
  target_link_libraries(hrrr_fvcom.exe PRIVATE OpenMP::OpenMP_Fortran)
endif()

install(
  TARGETS hrrr_fvcom.exe
  EXPORT ${PROJECT_NAME}Exports
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
