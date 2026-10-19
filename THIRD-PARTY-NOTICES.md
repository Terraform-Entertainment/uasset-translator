# Third-party notices

UassetTranslator, copyright (c) 2026 Terraform Entertainment, includes the open-source components below. Each is
used under its license, and the full license texts are in the `licenses` folder that ships with the Software.

| Component | License | Copyright | License text |
|---|---|---|---|
| UAssetAPI (modified; see below) | MIT | Copyright (c) 2020 - 2026 atenfyr | `licenses/UAssetAPI-LICENSE.txt` |
| Code that UAssetAPI includes: repak, Json.NET, dotmore, ZstdNet, zstd, CUE4Parse, UEAssetToolkitGenerator | MIT, BSD-3-Clause, Apache-2.0 | See the notice file | `licenses/UAssetAPI-NOTICE.md` |
| Newtonsoft.Json 13.0.4 | MIT | Copyright (c) 2007 James Newton-King | `licenses/Newtonsoft.Json-LICENSE.md` |
| ZstdSharp.Port 0.8.1 (a port of zstd) | MIT; zstd is BSD-3-Clause | Copyright (c) Oleg Stepanischev; zstd: Copyright (c) Meta Platforms, Inc. and affiliates | `licenses/ZstdSharp-LICENSE.txt`, and the zstd section of `licenses/UAssetAPI-NOTICE.md` |
| xxHash 0.8.0 (XXH3-64, ported to C#) | BSD-2-Clause | Copyright (c) 2012-2020 Yann Collet | `licenses/xxHash-LICENSE.txt` |
| .NET runtime 10.0 (bundled in `uasset.exe`) | MIT | Copyright (c) .NET Foundation and Contributors | `licenses/dotnet-LICENSE.txt`, and its own notices in `licenses/dotnet-THIRD-PARTY-NOTICES.txt` |

UAssetAPI is modified by Terraform Entertainment to support Unreal Engine 5.8 packages: import type hierarchies,
localization metadata, FText DevNotes, script serialization offsets, shared file access and a payload offset
accessor.

To convert audio as the editor does, the Software loads the libsndfile library (LGPL-2.1) that ships with the user's
Unreal Engine installation (Engine/Binaries/ThirdParty/libsndfile). The Software does not include or distribute it.

To read data the editor stores compressed, the Software loads the Oodle library (oo2core) that ships with the user's
Unreal Engine installation (in its .NET tools under Engine/Binaries/DotNET), under the user's Unreal Engine license. The
Software does not include or distribute it.

Unreal and Unreal Engine are trademarks or registered trademarks of Epic Games, Inc. Claude and Claude Code are
trademarks of Anthropic, PBC. UassetTranslator is not affiliated with, sponsored by, or endorsed by either company.
