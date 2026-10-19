# Privacy

UassetTranslator runs entirely on your computer.

- It sends nothing about your work anywhere. There is no telemetry, analytics, crash reporting or update check.
- It contacts the license server (shop.terraformentertainment.com) only when you activate a license, when the free
  trial starts (your first Pro command without a license) and when you remove a license. It sends your license key
  (when activating), a computer ID made of three hashes of this computer's identifiers (unique to this product, so it
  can't be linked to other apps), the program version and the computer's name. `uasset activate --offline` activates
  without any connection from this computer.
- After that, the license is checked offline against a public key built into the program. It is stored in
  `%LOCALAPPDATA%\TerraformEntertainment\UassetTranslator`.
- Edits are backed up inside your own project, in `Saved/UassetTranslator/Backups`.
- `uasset validate` starts the Unreal Editor installed on your computer. It uses a scratch project in
  `%LOCALAPPDATA%\UassetTranslator\Validation`, or, with `--in-project`, your project. It writes its log to that
  project's `Saved/UassetTranslator` folder.

Your AI agent sees the text that `uasset` prints, as it sees any command output. What your agent's provider does with
it is covered by that provider's terms.

When you buy a license, Paddle processes the payment and handles your payment details under its own privacy policy.
Terraform Entertainment receives the details needed to issue and support your license (your name and email address,
shown as "Licensed to").

Questions about privacy: support@terraformentertainment.com.
