# PCSX2-Sanity

A modified build of PCSX2 that incorporates changes that would be rejected from the parent repository. Only Jak and Daxter things for now, but can be used for anything.

If you have any changes that you think would improve the emulator but would get rejected (or did already get rejected) from the parent repository, feel free to open a pull request, or contact the maintainer of pcsx2-sanity: [LuminarLight](https://github.com/LuminarLight)

### Current divergences from parent repository
- Included 'Sanity' in the application's name at most places.
- Reworked the auto-updater. It no longer exclusively relies on the unique API on the PCSX2 website, it now also supports GitHub API.
- If a 'DRIVERS\FIREWIRE.IRX' or a 'DISKINFO.BIN' file exists on the disc, then it will be treated as the main ELF for booting and CRC purposes. If neither are found, the old behaviour will be used (looking up 'SYSTEM.CNF' and getting ELF path from there). This had to be done because in Jak pre-release builds, the "official" ELF is just a loader for these files, and this loader is usually fully identical between different pre-release builds of the same Jak game, which means they also have same CRC, making patches and everything impossible. But the FIREWIRE.IRX and DISKINFO.BIN files are (almost always) unique, allowing us to uniquely identify these builds. A nice side-effect of booting these files directly is that we completely bypass the WIBU protection.
- Imported and reworked the Jak Debug Mode patches from the [128MB Build](https://github.com/xTVaser/pcsx2-rr/tree/128mb-build) (the author field was filled where it was determinable, otherwise it was left empty - please contact me if there are any mistakes in this.
  - Numerous new Debug Mode patches have also been added, on top of the ones that were already in the 128MB Build.
- When the 'Advanced->Enable Extended RAM (Dev Console)' setting is enabled, all patches labelled as `[TOOL]` will be automatically loaded.
  - When a Jak game is booted in Debug Mode, the memory changes significantly. This means that patches made for the game running in normal mode corrupt the game when running in Debug Mode. So if the above setting is enabled, the emulator will attempt to load patches with `Widescreen 16:9 TOOL` and `No-Interlacing TOOL` labels instead of their TOOL-less counterparts, but only if all other conditions are met (for example the setting that force-loads widescreen patches).
- When you look at the patches of a game, normally it doesn't indicate whether a patch would get auto-loaded due to global settings or not. Now there is an indicator for this - if a patch will get loaded due to global settings, it will be highlighted in green in the list. This is especially useful if you want to have a clear picture when you are using the patch segregation features.
- GitHub releases for the project are no longer automatic. I think manual is better for a project like this.
- Assign serial code 'X' to ISOs where we treat FIREWIRE.IRX or DISKINFO.BIN as the main ELF. Because per-game settings for some reason don't work if the serial is empty.
- Made the 'Show Cheats For All CRCs' and 'Show Patches For All CRCs' settings never work, because it was causing big issues and I do not believe that it would ever be useful for anything. So as a safeguard, I have made it act as disabled regardless of the actual setting.
- Added gamefixes for various Jak and Daxter pre-release builds, into GameIndex.yaml. The parent repository does not allow such gamefixes to be included, so we had to do it here.
- Made the 'patches' directory always be checked from the app root. We had to do this, because we ship patches in that folder and it is next to the executable.

### Plans/TODO:
- Properly get the serial even if we use FIREWIRE.IRX or DISKINFO.BIN as main ELF for an ISO.
- Prevent non-labelled patches. This is PCSX2-Sanity, we can expect our users to adapt their pnach files. In most cases they just have to add one line to the top of the file.
- Readd the ability to broadcast a custom message into the auto-updater window. It could be useful.


And here is the parent's README:
---

# PCSX2

![Windows Build Status](https://img.shields.io/github/actions/workflow/status/PCSX2/pcsx2/windows_build_matrix.yml?label=%F0%9F%96%A5%EF%B8%8F%20Windows%20Builds)
![Linux Build Status](https://img.shields.io/github/actions/workflow/status/PCSX2/pcsx2/linux_build_matrix.yml?label=%F0%9F%90%A7%20Linux%20Builds)
![MacOS Build Status](https://img.shields.io/github/actions/workflow/status/PCSX2/pcsx2/macos_build_matrix.yml?label=%F0%9F%8D%8E%20MacOS%20Builds)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/1f7c0d75fec74d6daa6adb084e5b4f71)](https://app.codacy.com/gh/PCSX2/pcsx2/dashboard?utm_source=github.com&utm_medium=referral&utm_content=PCSX2/pcsx2&utm_campaign=Badge_Grade)
[![Discord Server](https://img.shields.io/discord/309643527816609793?color=%235CA8FA&label=PCSX2%20Discord&logo=discord&logoColor=white)](https://discord.com/invite/TCz3t9k)

PCSX2 is a free and open-source PlayStation 2 (PS2) emulator. Its purpose is to emulate the PS2's hardware, using a combination of MIPS CPU [Interpreters](<https://en.wikipedia.org/wiki/Interpreter_(computing)>), [Recompilers](https://en.wikipedia.org/wiki/Dynamic_recompilation) and a [Virtual Machine](https://en.wikipedia.org/wiki/Virtual_machine) which manages hardware states and PS2 system memory. This allows you to play PS2 games on your PC, with many additional features and benefits.

## Project Details

PCSX2 has been in development for more than 20 years. Past versions could only run a few public domain game demos, but newer versions can run most games at full speed, including popular titles such as Final Fantasy X and Devil May Cry 3. Visit the [PCSX2 compatibility list](https://pcsx2.net/compat/) to check the latest compatibility status of games (with more than 2500 titles tested).

Installers and binaries for both stable and nightly builds are available from [our website](https://pcsx2.net/downloads/).

## System Requirements

PCSX2 supports Windows, Linux, and Mac platforms. Our [setup documentation page](https://pcsx2.net/docs/setup/requirements) contains additional details on software and hardware requirements.

Please note that a BIOS dump from a legitimately-owned PS2 console is required to use the emulator. For more information, visit [this page](https://pcsx2.net/docs/setup/bios/).

## Contributing / Building

PCSX2 supports translation into other languages using [Crowdin](https://crowdin.com/project/pcsx2-emulator).

See the [Contribution Guide](https://pcsx2.net/docs/contributing/) for more info on how to contribute.
