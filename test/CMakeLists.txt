if(NOT MSVC)
  add_library(static_lib lib.cc)
  target_link_libraries(static_lib PUBLIC fmt::fmt)

  add_library(static_header_lib lib.cc)
  target_compile_definitions(static_header_lib PUBLIC FMTLOG_HEADER_ONLY)
  target_link_libraries(static_header_lib PUBLIC fmt::fmt)

  add_library(shared_lib SHARED lib.cc)
  target_link_libraries(shared_lib PUBLIC fmt::fmt)
  install(TARGETS shared_lib)

  add_library(shared_header_lib SHARED lib.cc)
  target_compile_definitions(shared_header_lib PUBLIC FMTLOG_HEADER_ONLY)
  target_link_libraries(shared_header_lib PUBLIC fmt::fmt)
  install(TARGETS shared_header_lib)

  add_executable(link_static_static link_test.cc)
  target_link_libraries(link_static_static fmtlog-static static_lib fmt::fmt)
  install(TARGETS link_static_static)

  add_executable(link_static_shared link_test.cc)
  target_link_libraries(link_static_shared fmtlog-static shared_lib fmt::fmt)
  install(TARGETS link_static_shared)

  add_executable(link_shared_static link_test.cc)
  target_link_libraries(link_shared_static fmtlog-shared static_lib fmt::fmt)
  install(TARGETS link_shared_static)

  add_executable(link_shared_shared link_test.cc)
  target_link_libraries(link_shared_shared fmtlog-shared shared_lib fmt::fmt)
  install(TARGETS link_shared_shared)

  add_executable(link_header_static link_test.cc)
  target_link_libraries(link_header_static static_header_lib fmt::fmt)
  install(TARGETS link_header_static)

  add_executable(link_header_shared link_test.cc)
  target_link_libraries(link_header_shared shared_header_lib fmt::fmt)
  install(TARGETS link_header_shared)

endif()

add_executable(log_test log_test.cc)
target_link_libraries(log_test fmtlog-static fmt::fmt)
#target_compile_definitions(log_test PUBLIC FMTLOG_HEADER_ONLY)
install(TARGETS log_test)

add_executable(enc_dec_test enc_dec_test.cc)
target_link_libraries(enc_dec_test fmtlog-static fmt::fmt)
install(TARGETS enc_dec_test)

add_executable(multithread_test multithread_test.cc)
target_compile_definitions(multithread_test PUBLIC FMTLOG_HEADER_ONLY)
target_link_libraries(multithread_test PUBLIC fmt::fmt)
install(TARGETS multithread_test)

