# Ansible Role: Fonts
[![CI](https://github.com/skaary/ansible-role-fonts/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/skaary/ansible-role-fonts/actions?query=workflow%3Ci)

An Ansible Role that installs [Powerline fonts](https://github.com/powerline/fonts) and [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts#font-installation) on Linux.

Nerd Fonts are individually downloaded directly from GitHub; this role does not clone the whole repository to reduce waste.

## Requirements

None

## Role Variables

| Variable name                 | Default value | Description |
|-------------------------------|---------------|-------------|
| `fonts_user`                     | `""`            | The name of the user to install the fonts for. Required. |
| `fonts_group`                    | `""`            | The group of the user to install the fonts for. Required. |
| `fonts_directory`          | `/home/{{ fonts_user }}/.local/share/fonts` | The default location to install fonts on Linux systems. |
| `nerdfonts_directory`          | `/home/{{ fonts_user }}/.local/share/fonts/NerdFonts` | The default location to install Nerd Fonts on Linux systems. |
| `nerdfonts_github_raw_patched_fonts` | `https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts` | The remote directory from which to download raw Nerd Font files. |
| `nerdfonts_single_fonts`             | `[]` | A list of paths to individual Nerd Fonts to download, relative to `nerdfonts_github_raw_patched_fonts` (see Example Playbook below). Required. |

## Dependencies

None

## Example Playbook

```yaml
---
- name: Ansible Role Fonts Example Playbook
  hosts: all
  vars:
    fonts_user: "molecule"
    fonts_group: "{{ nf_user }}"
    nerdfonts_single_fonts:
     - "UbuntuMono/Regular/complete/Ubuntu Mono Nerd Font Complete.ttf"
     - "AurulentSansMono/complete/AurulentSansMono-Regular Nerd Font Complete.otf"
  tasks:
    - name: "Include ansible-role-fonts"
      include_role:
        name: "ansible-role-fonts"
```

## License

