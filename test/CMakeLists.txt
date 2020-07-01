enable_testing()

add_executable(blake2_test test_main.c)
add_test(NAME blake2_test COMMAND blake2_test)
target_link_libraries(blake2_test blake2)