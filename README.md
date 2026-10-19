# UAsset Translator

**Let your AI coding agent read and change Unreal Engine Blueprints and assets. No editor required.**

Ask Claude Code (or any agent that runs commands) about your project in your own words: "why doesn't my door open?",
"add a sprint on Shift", "put five lights along the corridor". The agent reads the assets as text, makes the change,
and checks it in the engine. There are no commands for you to learn.

![The same Blueprint before and after one layout command](https://github.com/terraform-entertainment/uasset-translator/releases/download/v0.2.2/before-after.png)

**[Quick Start](https://terraformentertainment.com/uassettranslator/quickstart/)** Â·
**[Documentation](https://terraformentertainment.com/uassettranslator/docs/)** Â·
**[Changelog](CHANGELOG.md)**

## Install

**Claude Code**, in a terminal (the plugin brings the tool with it):

```
claude plugin install uasset-translator --marketplace terraform-entertainment/uasset-translator
```

Then open your Unreal project folder in Claude Code and start talking.

**Other agents** (Cursor, Codex, Antigravity, Copilot, Windsurf...): install the `uasset` command one of three ways.
Each puts it on your PATH, and running it again updates it.

1. **PowerShell**, one line:

   ```
   irm https://github.com/terraform-entertainment/uasset-translator/releases/latest/download/install.ps1 | iex
   ```

2. **winget** (once Microsoft's review of the listing is done):

   ```
   winget install TerraformEntertainment.UassetTranslator
   ```

3. **Installer**: download `uasset-translator-<version>-setup.exe` from [Releases](../../releases/latest) and run it.
   No administrator rights needed, and it can add the Claude Code plugin too. It isn't code-signed yet, so Windows
   may say "Windows protected your PC": choose **More info**, then **Run anyway**. Remove it in Settings > Apps.

Then, in each Unreal project, run `uasset agents-md` to give your agent the instructions.

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
