esma_set_this ()

set (gsdchem_srcs
  aero_soa_vbs_data_mod.F90
  dep_dry_gocart_mod.F90
  dep_dry_mod.F90
  dep_simple_mod.F90
  dep_vertmx_mod.F90
  dep_wet_ls_mod.F90
  dust_afwa_mod.F90
  dust_data_mod.F90
  dust_fengsha_mod.F90
  dust_gocart_mod.F90
  gocart_aerosols_mod.F90
  gocart_chem_mod.F90
  gocart_diag_mod.F90
  gocart_dmsemis_mod.F90
  gocart_settling_mod.F90
  gsd_chem_config.F90
  gsd_chem_constants.F90
  opt_aer_mod.F90
  opt_aer_out_mod.F90
  opt_aer_ra_mod.F90
  opt_averaging_mod.F90
  opt_data_mod.F90
  opt_driver_mod.F90
  opt_gocart_mod.F90
  opt_mod.F90
  plume_data_mod.F90
  plume_rise_mod.F90
  plume_scalar_mod.F90
  plume_zero_mod.F90
  seas_data_mod.F90
  seas_mod.F90
  seas_ngac_mod.F90
  vash_settling_mod.F90
)

set (srcs
  Chem_MieTableMod2G.F90
  GOCART2G_Process.F90
  ${gsdchem_srcs}
  )

# Force 64bit for original gsdchem files for now, because they are just too hard to change
if(CMAKE_Fortran_COMPILER_ID MATCHES "Intel")
  set (CMAKE_Fortran_FLAGS_64bit "${CMAKE_Fortran_FLAGS} -i4 -real-size 64")
elseif(CMAKE_Fortran_COMPILER_ID MATCHES "GNU")
  set(CMAKE_Fortran_FLAGS_64bit "${CMAKE_Fortran_FLAGS} -fdefault-real-8")
endif()
SET_SOURCE_FILES_PROPERTIES(${gsdchem_srcs} PROPERTIES COMPILE_FLAGS "${CMAKE_Fortran_FLAGS_64bit}")

esma_add_library(${this} 
  SRCS ${srcs} 
  DEPENDENCIES esmf NetCDF::NetCDF_Fortran
  )
