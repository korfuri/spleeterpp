add_library(spleeter_filter
  model.h
  model.cc
  filter.cc
  filter.h
  tensor.h
  tensor.cc
)

find_package(PkgConfig REQUIRED)
pkg_search_module(EIGEN REQUIRED eigen3 IMPORTED_TARGET)
pkg_search_module(TENSORFLOW REQUIRED tensorflow IMPORTED_TARGET)

target_link_libraries(spleeter_filter ${EIGEN_LIBRARIES} ${TENSORFLOW_LIBRARIES})
target_include_directories(spleeter_filter PUBLIC ${EIGEN_INCLUDE_DIRS} ${TENSORFLOW_DIRS})
target_compile_options(spleeter_filter PUBLIC ${EIGEN_CFLAGS_OTHER} ${TENSORFLOW_CFLAGS_OTHER})

target_link_libraries(spleeter_filter
  spleeter_common
  artff
)

target_compile_definitions(spleeter_filter
  PRIVATE
    SPLEETER_INPUT_FRAME_COUNT=${spleeter_input_frame_count}
)

install(TARGETS spleeter_filter
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)
install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/filter.h
  DESTINATION include/spleeter_filter
)

# Also install the pretrained models
install(DIRECTORY
  ${spleeter_filter_models_dir}/
  DESTINATION models/filter
)
