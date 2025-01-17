## :children_crossing: Disclaimer :framed_picture: :potable_water:

**This repository is used as part of The Water Museum's internal build processes for games. It is not necessarily intended for public use or consumption, as the underlying code may contain changes that are specific to our needs and environments.** While you're welcome to adapt our public projects to your own use cases, we are unable to offer additional support or guidance.

At times, specific improvements and features from our internal forks may be backported to their sources. Thus, we strongly recommend using the original upstream repository for your projects.

# steam-totp

[![Test](https://github.com/CyberAndrii/steam-totp/workflows/Test/badge.svg)](https://github.com/CyberAndrii/steam-totp/actions)
[![License: MIT](https://img.shields.io/github/license/CyberAndrii/steam-totp?label=License)](LICENSE)

This action generates Steam's two factor auth codes for use in actions.

# Usage

The following example logins into SteamCMD.

```yaml
steps:
- name: Setup steamcmd
  uses: CyberAndrii/setup-steamcmd@v1
  
- name: Generate auth code
  id: generate
  uses: CyberAndrii/steam-totp@v1
  with:
    shared_secret: ${{ secrets.STEAM_SHARED_SECRET }}
  
- run: steamcmd +login ${{ secrets.STEAM_USERNAME }} ${{ secrets.STEAM_PASSWORD }} ${{ steps.generate.outputs.code }} +quit
 ```
 
 It also uses [setup-steamcmd](https://github.com/CyberAndrii/setup-steamcmd) action.
 
# Inputs

| name          | description                                                   | required | default |
|---------------|---------------------------------------------------------------|----------|---------|
| shared_secret | Shared secret from the .maFile.                               | true     |         |
| time_offset   | The number of seconds that will be added to the current time. | false    | 0       |

# Outputs

| name | description          |
|------|----------------------|
| code | Generated auth code. |
