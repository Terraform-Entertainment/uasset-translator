# UAsset Translator

**Let your AI coding agent read and change Unreal Engine Blueprints and assets. No editor required.**

Ask Claude Code (or any agent that runs commands) about your project in your own words: "why doesn't my door open?",
"add a sprint on Shift", "put five lights along the corridor". The agent reads the assets as text, makes the change,
and checks it in the engine. There are no commands for you to learn.

![The same Blueprint before and after one layout command](https://github.com/terraform-entertainment/uasset-translator/releases/download/v0.2.1/before-after.png)

**[Quick Start](https://terraformentertainment.com/uassettranslator/quickstart/)** ·
**[Documentation](https://terraformentertainment.com/uassettranslator/docs/)** ·
**[Changelog](CHANGELOG.md)**

## Install

Claude Code on Windows, in a terminal:

```
claude plugin install uasset-translator --marketplace terraform-entertainment/uasset-translator
```

Then open your Unreal project folder in Claude Code and start talking.

Other agents (Cursor, Codex, Antigravity, Copilot, Windsurf...), in PowerShell:

```
irm https://github.com/terraform-entertainment/uasset-translator/releases/latest/download/install.ps1 | iex
```

It installs `uasset.exe` and puts it on your PATH (run it again to update). Then, in each Unreal project, run
`uasset agents-md` to give your agent the instructions. Or download the zip from [Releases](../../releases) and follow
[Install](https://terraformentertainment.com/uassettranslator/docs/#install) in the documentation.

Windows 10 or 11, x64. Project files saved by Unreal Engine 5.8. The engine check needs the project's Unreal Engine
version installed.

<a id="buy"></a>
## Free and Pro

Reading your project and looking up what the engine offers are free. Changing assets and the engine check are Pro,
free for 14 days from first use.

**[Buy UAsset Translator Pro](https://terraformentertainment.com/uassettranslator/)**: a perpetual license per
person, with 12 months of updates. Activate the key in a terminal yourself (not in an AI chat), once on each of your
computers:

```
uasset activate <key>
```

## Support

Open an issue in this repository, or use the
[support page](https://terraformentertainment.com/support/). Email: support@terraformentertainment.com.

Found a bug? Run `uasset bug-report` and email the file it writes to bugs@terraformentertainment.com. The tool never
sends anything by itself.

---

Copyright (c) 2026 Terraform Entertainment. All rights reserved. Use is governed by the [EULA](EULA.md). Everything
runs on your computer and sends nothing anywhere: see [PRIVACY.md](PRIVACY.md). Third-party components:
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

Unreal and Unreal Engine are trademarks or registered trademarks of Epic Games, Inc. Claude and Claude Code are
trademarks of Anthropic, PBC. UAsset Translator is not affiliated with, sponsored by, or endorsed by either company.
