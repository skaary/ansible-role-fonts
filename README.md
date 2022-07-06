# Ansible Role: Fonts
[![CI](https://github.com/skaary/ansible-role-fonts/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/skaary/ansible-role-fonts/actions?query=workflow%3Ci)

An Ansible Role that installs existing fonts from the apt repository and [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts#font-installation) on Linux.

Nerd Fonts are individually downloaded directly from GitHub; this role does not clone the whole repository to reduce waste.

## Installation

Download the role directly from git by typing into your terminal:

```bash
$ ansible-galaxy install git+https://github.com/skaary/ansible-role-fonts.git
```

or

```bash
$ ansible-galaxy install git+https://github.com/skaary/ansible-role-fonts.git,,fonts
```

to change the installed role name from _ansible-role-fonts_ to just _fonts_.

Alternatively, install the role via a _requirements.yml_ file, e.g. when installing multiple roles at once. See [ansible galaxy documentation](https://galaxy.ansible.com/docs/using/installing.html#installing-multiple-roles-from-a-file) for more information.

## Role Variables

| Variable name                        | Default value                                                      | Description                                                                                                                                    |
| ------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `fonts_user`                         | `""`                                                               | The name of the user to install the fonts for. Required.                                                                                       |
| `fonts_group`                        | `""`                                                               | The group of the user to install the fonts for. Required.                                                                                      |
| `fonts_directory`                    | `/home/{{ fonts_user }}/.local/share/fonts`                        | The default location to install fonts to.                                                                                                      |
| `fonts_repository`                   | `[]`                                                               | A list of fonts that are available from the apt repository to install.                                                                         |
| `nerdfonts_directory`                | `/home/{{ fonts_user }}/.local/share/fonts/NerdFonts`              | The default location to install Nerd Fonts to.                                                                                                 |
| `nerdfonts_github_raw_patched_fonts` | `https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts` | The remote directory from which to download raw Nerd Font files.                                                                               |
| `nerdfonts_single_fonts`             | `[]`                                                               | A list of paths to individual Nerd Fonts to download, relative to `nerdfonts_github_raw_patched_fonts` (see Example Playbook below). Required. |
<!-- | `droid_sans_mono_directory           | `"{{ fonts_directory }}/droid-sans-mono"`                          | The default location to install Droid Sans Mono Fonts to.                                                                                      |
| `droid_sans_mono_fonts`              | `[]`                                                               | A list of paths to individual Nerd Fonts to download, relative to `nerdfonts_github_raw_patched_fonts` (see Example Playbook below). Required. | -->

## Example Playbook

```yaml
---
- name: Ansible Role Fonts Example Playbook
  hosts: all
  vars:
    fonts_user: "skaary"
    fonts_group: "{{ nf_user }}"
    fonts_repository:
     - fonts-powerline
     - fonts-liberation
    nerdfonts_single_fonts:
     - "UbuntuMono/Regular/complete/Ubuntu Mono Nerd Font Complete.ttf"
     - "AurulentSansMono/complete/AurulentSansMono-Regular Nerd Font Complete.otf"
  tasks:
    - name: "Include ansible-role-fonts"
      include_role:
        name: "ansible-role-fonts"
```

# Testing the role

### Vagrant

Vagrant can be used to test the role in order to graphically see it working in a virtual machine. Make sure Vagrant and VirtualBox are installed:

```bash
$ sudo apt install vagrant virtualbox
```

Use the following commands to run vagrant and boot up the virtual machine:

```bash
$ cd tests
$ vagrant up
```

Use `vagrant destroy` after you are done testing to delete the virtual machine. For more information about Vagrant and its commands, see the [Vagrant documentation](https://www.vagrantup.com/docs/cli).

### Molecule with Docker

Molecule can be used to test the role with a docker container. Make sure Molecule is installed:

```bash
$ python3 -m pip install --user "molecule[docker]"
```

Use the following commands to run Molecule in order to create the docker container and access the created container:
```bash
$ molecule converge && molecule login
```

For more information on how to use Molecule please consult the [Molecule documentation](https://molecule.readthedocs.io/en/latest/getting-started.html).

> Note: Python and Docker are required for the use of molecule. For more information, see [Molecule installation](https://molecule.readthedocs.io/en/latest/installation.html).

## License

MIT / BSD
