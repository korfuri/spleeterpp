add_library(spleeter_common
  type.h
  registry.h
  registry.cc
  tf_handle.h
  tf_handle.cc
  spleeter_common.h
  spleeter_common.cc
)

find_package(PkgConfig REQUIRED)
pkg_search_module(EIGEN REQUIRED eigen3 IMPORTED_TARGET)
pkg_search_module(TENSORFLOW REQUIRED tensorflow IMPORTED_TARGET)

target_link_libraries(spleeter_common ${EIGEN_LIBRARIES} ${TENSORFLOW_LIBRARIES})
target_include_directories(spleeter_common PUBLIC ${EIGEN_INCLUDE_DIRS} ${TENSORFLOW_DIRS})
target_compile_options(spleeter_common PUBLIC ${EIGEN_CFLAGS_OTHER} ${TENSORFLOW_CFLAGS_OTHER})


# target_link_libraries(spleeter_common
#   tensorflow
#   Eigen3::Eigen
# )

install(TARGETS spleeter_common
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)

install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/spleeter_common.h
  ${CMAKE_CURRENT_SOURCE_DIR}/type.h
  DESTINATION include/spleeter_common/
)
