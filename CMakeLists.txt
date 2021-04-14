cmake_minimum_required(VERSION 3.17)

set(CMAKE_CXX_STANDARD 17)
# this is the source of truth for semver version
project(ci_test VERSION 1.3.0)

# for main line release, this is empty
# for development release, this is "-develop"
# for release candidate, this is "-rc"
set(PROJ_PRERELEASE "-develop")

# these are computed
set(PROJ_VERSION_NUM "${PROJECT_VERSION}${PROJ_PRERELEASE}")
set(PROJ_VERSION "ci-test ${PROJECT_VERSION}${PROJ_PRERELEASE}")

# used in CI
file(WRITE ${CMAKE_BINARY_DIR}/VERSION ${PROJ_VERSION_NUM})

add_executable(ci_test main.cpp)