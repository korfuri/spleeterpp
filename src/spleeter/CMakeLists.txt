add_library(spleeter
  model.cc
  model.h
  spleeter.cc
  spleeter.h
)

find_package(PkgConfig REQUIRED)
pkg_search_module(EIGEN REQUIRED eigen3 IMPORTED_TARGET)

target_link_libraries(spleeter ${EIGEN_LIBRARIES})
target_include_directories(spleeter PUBLIC ${EIGEN_INCLUDE_DIRS})
target_compile_options(spleeter PUBLIC ${EIGEN_CFLAGS_OTHER})

target_link_libraries(spleeter
  spleeter_common
)

install(TARGETS spleeter
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)

install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/spleeter.h
  DESTINATION include/spleeter/
)

# Also install the pretrained models
install(DIRECTORY
  ${spleeter_models_dir}/
  DESTINATION models/default
)
