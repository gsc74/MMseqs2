cmake_minimum_required(VERSION 3.15)
project(tinyexpr C)

option(TE_POW_FROM_RIGHT "Evaluate exponents from right to left." OFF)
option(TE_NAT_LOG "Define the log function as natural logarithm." OFF)
option(build_tinyexpr_test "Build TinyExpr tests." OFF)
option(build_tinyexpr_test_pr "Build TinyExpr tests PR." OFF)
option(build_tinyexpr_bench "Build TinyExpr benchmark." OFF)
option(build_tinyexpr_example "Build TinyExpr example." OFF)
option(build_tinyexpr_example2 "Build TinyExpr example 2." OFF)
option(build_tinyexpr_example3 "Build TinyExpr example 3." OFF)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -ansi -Wall -Wshadow -fPIC -O3")

set(SOURCE_FILES
        tinyexpr.c
        tinyexpr.h
        )

add_library(tinyexpr STATIC ${SOURCE_FILES})
set_target_properties(tinyexpr PROPERTIES COMPILE_FLAGS "${MMSEQS_C_FLAGS}" LINK_FLAGS "${MMSEQS_C_FLAGS}")
if (TE_POW_FROM_RIGHT)
    target_compile_definitions(tinyexpr PRIVATE TE_POW_FROM_RIGHT)
endif()
if (TE_NAT_LOG)
    target_compile_definitions(tinyexpr PRIVATE TE_NAT_LOG)
endif()
install(TARGETS tinyexpr ARCHIVE DESTINATION lib)
install(FILES tinyexpr.h DESTINATION include COMPONENT Devel)

if (build_tinyexpr_test)
    add_executable(tinyexpr_test test.c tinyexpr.c)
endif()

if (build_tinyexpr_test_pr)
    add_executable(tinyexpr_test_pr test.c tinyexpr.c)
    target_compile_definitions(tinyexpr_test_pr PRIVATE TE_POW_FROM_RIGHT TE_NAT_LOG)
endif()

if (build_tinyexpr_bench)
    add_executable(tinyexpr_benchmark benchmark.c tinyexpr.c)
endif()

if (build_tinyexpr_example)
    add_executable(tinyexpr_example example.c tinyexpr.c)
endif()

if (build_tinyexpr_example2)
    add_executable(tinyexpr_example2 example2.c tinyexpr.c)
endif()

if (build_tinyexpr_example3)
    add_executable(tinyexpr_example3 example3.c tinyexpr.c)
endif()
