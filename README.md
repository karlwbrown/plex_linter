[![made-with-python](https://img.shields.io/badge/Made%20with-Python-blue.svg?style=flat-square)](https://www.python.org/)
[![License: GPL v3](https://img.shields.io/badge/License-GPL%203-blue.svg?style=flat-square)](https://github.com/karlwbrown/plex_linter/blob/master/LICENSE.md)
[![Contributing](https://img.shields.io/badge/Contributing-gray.svg?style=flat-square)](CONTRIBUTING.md)

---

<!-- TOC depthFrom:1 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
  - [Sample](#sample)
  - [Plex](#plex)
- [Usage](#usage)
- [Inspiration](#inspiration)

<!-- /TOC -->

---

# Introduction

Plex Linter is a python script that looks for various potential issues in your library, such as 
  * Duplicate album titles (that could suggest albums that have been incorrectly split)
  * Duplicate artists (for artists that have been split)
  * Tracks without titles (sometimes Plex metadata deletes track titles)
  * Tracks linked to artists with Plex metadata that differ from what the MP3 tags say.

# Requirements

1. Python 3.8+.

1. Required Python modules (see below).


# Installation

_Note: Steps below are for Debian-based distros (other operating systems will require tweaking to the steps)._

1. Install Python 3 and PIP

   ```
   sudo apt install python3 python3-pip
   ```

1. Clone the Plex DupeFinder repo.

   ```
   sudo git clone https://github.com/karlwbrown/plex_linter /opt/plex_linter
   ```

1. Find your user & group.

   ```
   id
   ```

1. Fix permissions of the Plex Linter folder (replace `user`/`group` with yours).

   ```
   sudo chown -R user:group /opt/plex_linter
   ```

1. Go into the Plex Linter folder.

   ```
   cd /opt/plex_linter
   ```

1. Install the required python modules.

   ```
   sudo python3 -m pip install -r requirements.txt
   ```

1. Create a shortcut for Plex Linter.

   ```
   sudo ln -s /opt/plex_linter/plex_linter.py /usr/local/bin/plex_linter
   ```

1. Generate a `config.json` file.

   ```
   plex_linter
   ```

1. Fill in Plex URL and credentials at the prompt to generated a Plex Access Token (optional).

   ```
   Dumping default config to: /opt/plex_linter/config.json
   Plex Server URL: http://localhost:32400
   Plex Username: your_plex_username
   Plex Password: your_plex_password
   Please edit the default configuration before running again!
   ```

1. Configure the `config.json` file.

   ```
   nano config.json
   ```


# Configuration

## Sample

```json
  "PLEX_LIBRARIES": [
    "Music",
    "Audiobooks"
  ],
  "PLEX_SERVER": "https://plex.your-server.com",
  "PLEX_TOKEN": ""
}
```

## Plex

### Plex Libraries

1. Go to Plex and get all the names of your Plex Libraries you want to run the linter on

   - Example Library:

     ![](https://i.imgur.com/JFRTD1m.png)

1. Under `PLEX_LIBRARIES`, type in the Plex *Library Name* (exactly).

   - Format:

     ```
     "PLEX_LIBRARIES": [
       "LIBRARY_NAME_1"
       "LIBRARY_NAME_2"
     ],
     ```

### Plex Server URL

- Your Plex server's URL.

- This can be any format (e.g. <http://localhost:32400>, <https://plex.domain.ltd>).

### Plex Token

1. Obtain a Plex Access Token:

   - Fill in the Plex URL and Plex login credentials, at the prompt, on first run. This only occurs when there is no `config.json` present.

     or

   - Visit https://support.plex.tv/hc/en-us/articles/204059436-Finding-an-authentication-token-X-Plex-Token

1. Add the Plex Access Token to `"PLEX_TOKEN"` so that it now appears as `"PLEX_TOKEN": "abcd1234",`.

   - Note: Make sure it is within the quotes (`"`) and there is a comma (`,`) after it.


# Usage

Simply run the script/command:

```
plex_dupefinder
```

***

# Inspiration

This project started as a fork of https://github.com/l3uddz/plex_dupefinder and used a lot of that code as a starting point.

