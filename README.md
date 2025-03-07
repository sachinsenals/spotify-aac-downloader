# Spotify ✨ AAC ✨ Downloader
A Python script to download songs/albums/playlists directly from Spotify in 256kbps/128kbps AAC.

## Setup
1. Install Python 3.7 or newer
2. Install spotify-aac-downloader with pip
    ```
    pip install spotify-aac-downloader
    ```
3. Add [FFmpeg](https://ffmpeg.org/download.html) to PATH or specify the location using the command line arguments or the config file (see [Configuration](#configuration))
4. Place your cookies in the same folder that you will run the script as `cookies.txt`
    * You can export your cookies by using this Google Chrome extension on Spotify website: https://chrome.google.com/webstore/detail/open-cookiestxt/gdocmgbfkjnnpapoeobnolbbkoibbcif. Make sure to be logged in.
5. Place your .wvd file in the same folder that you will run the script as `device.wvd`
    * You can use [dumper](https://github.com/wvdumper/dumper) to dump your phone's L3 CDM. Once you have the L3 CDM, use pywidevine to create the .wvd file from it.
        1. Install pywidevine with pip
            ```
            pip install pywidevine pyyaml
            ```
        2. Create the .wvd file
            ```
            pywidevine create-device -t ANDROID -l 3 -k private_key.pem -c client_id.bin -o .
            ```

## Configuration
spotify-aac-downloader can be configured using the command line arguments or the config file. The config file is created automatically when you run spotify-aac-downloader for the first time at `~/.spotify-aac-downloader/config.json` on Linux and `%USERPROFILE%\.spotify-aac-downloader\config.json` on Windows. Config file values can be overridden using command line arguments.
| Command line argument / Config file key | Description | Default value |
| --- | --- | --- |
| `-f,`, `--final-path` / `final_path` | Path where the downloaded files will be saved. | `./Spotify` |
| `-t,`, `--temp-path` / `temp_path` | Path where the temporary files will be saved. | `./temp` |
| `-c,`, `--cookies-location` / `cookies_location` | Location of the cookies file. | `./cookies.txt` |
| `-w,`, `--wvd-location` / `wvd_location` | Location of the .wvd file. | `./device.wvd` |
| `--ffmpeg-location` / `ffmpeg_location` | Location of the FFmpeg binary. | `ffmpeg` |
| `--config-location` / - | Location of the config file. | `<home>/.spotify-aac-downloader/config.json` |
| `--template-folder-album` / `template_folder_album` | Template of the album folders as a format string. | `{album_artist}/{album}` |
| `--template-folder-compilation` / `template_folder_compilation` | Template of the compilation album folders as a format string. | `Compilations/{album}` |
| `--template-file-single-disc` / `template_file_single_disc` | Template of the song files for single-disc albums as a format string. | `{track:02d} {title}` |
| `--template-file-multi-disc` / `template_file_multi_disc` | Template of the song files for multi-disc albums as a format string. | `{disc}-{track:02d} {title}` |
| `-e,`, `--exclude-tags` / `exclude_tags` | List of tags to exclude from file tagging separated by commas. | `null` |
| `--truncate` / `truncate` | Maximum length of the file/folder names. | `40` |
| `-l,`, `--log-level` / `log_level` | Log level. | `INFO` |
| `-p,`, `--premium-quality` / `premium_quality` | Download in 256kbps AAC instead of 128kbps AAC. | `false` |
| `-l,`, `--lrc-only` / `lrc_only` | Download only the synced lyrics. | `false` |
| `-n,`, `--no-lrc` / `no_lrc` | Don't download the synced lyrics. | `false` |
| `-s,`, `--save-cover` / `save_cover` | Save cover as a separate file. | `false` |
| `-o,`, `--overwrite` / `overwrite` | Overwrite existing files. | `false` |
| `--print-exceptions` / `print_exceptions` | Print exceptions. | `false` |
| `-u,`, `--url-txt` / - | Read URLs as location of text files containing URLs. | `false` |
| `-n,`, `--no-config-file` / - | Don't use the config file. | `false` |

### Tag variables
The following variables can be used in the template folder/file and/or in the `exclude_tags` list:
- `album`
- `album_artist`
- `artist`
- `comment`
- `compilation`
- `copyright`
- `cover`
- `disc`
- `disc_total`
- `lyrics`
- `media_type`
- `rating`
- `release_date`
- `release_year`
- `title`
- `track`
- `track_total`
