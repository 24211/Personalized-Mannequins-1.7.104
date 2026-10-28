Personalized Mannequins - 1.7.104
=================================

Unofficial rebuild of Personalized Mannequins for Skyrim SE 1.7.104.

Based on Personalized Mannequins by Adrien Melia (MIT License).
The original MIT license text is in LICENSE-MIT.txt.

This build links CommonLibSSE-NG v15.0.0, which is licensed under the
GNU General Public License v3.0. As a result, this build is distributed
under the GNU General Public License v3.0 as well.
See LICENSE in this repository for the full license text.

Copyright (C) 2022 Adrien Melia (original plugin source, MIT)
Copyright (C) 2026 xingyi (1.7.104 rebuild)

This program is free software: you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option)
any later version.

This program is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for
more details.

WHAT CHANGED
------------
* vcpkg overlay port commonlibsse-ng bumped from 3.6.0 to 15.0.0.
* Two API call sites migrated: CommonLibSSE-NG v15 removed
  GEOMETRY_RUNTIME_DATA::properties[] and States::kEffect; the shader
  property is now read via lightingShaderProp_cast().
* A null check was added on the material pointer.

No gameplay logic was changed.

WHY
---
The original DLL is rejected by SKSE 2.3.x on 1.7.x with
"must be recomplied for new address library", because the plugin version
structure lacks the AddressLibraryV5 bit (versionIndependenceEx 0x1
instead of 0x3).

Tested on Skyrim SE 1.7.104 only; other runtimes are untested.

AI DISCLOSURE
-------------
This rebuild was carried out under AI guidance. The AI did not edit files or
run builds: it analysed the SKSE load error, identified the API changes, and
supplied the exact edits and build commands. A human applied every edit, ran
every build, and performed all in-game testing.

BUILDING
--------
Requires Visual Studio with the vcpkg toolchain.

Configure:

  cmake -S . -B build/skyrim -G "Visual Studio 18 2026" -A x64 -DCMAKE_TOOLCHAIN_FILE=<vcpkg>/scripts/buildsystems/vcpkg.cmake -DVCPKG_OVERLAY_PORTS=<repo>/cmake/ports -DVCPKG_TARGET_TRIPLET=x64-windows-static-md -DBUILD_SKYRIM=ON

Build:

  cmake --build build/skyrim --config Release