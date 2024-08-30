# ansible-role-hosts-file

Ansible role for managing hosts files on a variety of operating systems

## Licence

Copyright 2024 Laurence Alexander Hurst

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

## What it does

Entries will be corrected or added for the addresses given, so the specified host name(s) resolve to them. Any entries resolving these hostnames to another address will be removed.

## Variables

The role uses these variables:

* `hosts_file_path` - the path to the hosts file (string). _Defaults to `/etc/host` on Linux, `{{ ansible_facts.SystemRoot }}\\System32\drivers\etc\hosts` on Windows and `/private/etc/hosts` on Darwin (macOS)._
* `hosts_file_hosts` - a list of entries to manage. Each entry is a dictionary consisting of:
  - `hostname` - hostname for the entry (string). _Required._
  - `add_short_nme` - If `hostname` is qualified (contains `.`), also add the short name (everything up to the first `.`) (boolean). _Defaults to `true`._
  - `ipv4` - IP version 4 specific options, a dictionary of:
    * `address` - IPv4 address for `hostname` to resolve to (string). _Required._
    * `aliases` - Additional aliases specific to the IPv4 address (list of strings). _Optional._
  - `ipv6` - IP version 6 specific options, a dictionary of:
    * `address` - IPv6 address for `hostname` to resolve to (string). _Required._
    * `aliases` - Additional aliases specific to the IPv6 address (list of strings). _Optional._

At least one of `ipv4` or `ipv6` must be provided for each `hosts_file_hsots`.


