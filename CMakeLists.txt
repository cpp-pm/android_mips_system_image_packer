# Copyright (c) 2018, Ruslan Baratov
# All rights reserved.

cmake_minimum_required(VERSION 3.3)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/09480ebda161be2a8e1b6c6c1a2810202219240f.zip"
    SHA1 "051ada419ac4d1bba0e7a6ad48c7999875a7b535"
)

project(android_mips_system_image_packer)

hunter_add_package(android_sdk_packer)

# android_sdk_packer_unified_install
# android_sdk_packer_parse_version_revision
find_package(android_sdk_packer CONFIG REQUIRED)

hunter_add_package(Android-MIPS-System-Image)
file(GLOB x "${ANDROID-MIPS-SYSTEM-IMAGE_ROOT}/*")
android_sdk_packer_parse_version_revision(
    FULL "${HUNTER_Android-MIPS-System-Image_VERSION}"
    VERSION version
    REVISION revision
)

android_sdk_packer_unified_install(
    OBJECTS ${x}
    DESTINATION "system-images/android-${version}/default/mips"
)
