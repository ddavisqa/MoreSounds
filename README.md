![SoundScrape!](http://i.imgur.com/nHAt2ow.png)

SoundScrape
==============

**SoundScrape** makes it easy to download artists from SoundCloud, Bandcamp, and Mixcloud—even tracks that don't have public download links. It automatically creates ID3 tags as well (including album art), which is handy.

This version has been modernized to run on Python 3.12+ and uses `yt-dlp` for robust Mixcloud support.

## Setup & Installation

This project is managed with `uv`.

First, install `uv`:
```bash
pip install uv
```

Next, clone the repository and set up the virtual environment:
```bash
git clone https://github.com/Miserlou/SoundScrape.git
cd SoundScrape
uv sync
```

### SoundCloud API Key

To download from SoundCloud, you must provide your own API key.

1.  Create a file named `.env` in the root of the project.
2.  Add your SoundCloud OAuth Token to the file like this:

    ```
    SOUNDCLOUD_CLIENT_ID="YOUR_TOKEN_HERE"
    ```

## Usage

To run `soundscrape`, use `uv run`:

```bash
uv run soundscrape rabbit-i-am
```
And you're done! Hooray! Files are stored as mp3s in the format **Artist name - Track title.mp3**.

You can also use the `-n` argument to only download a certain number of songs.

```bash
uv run soundscrape rabbit-i-am -n 3
```

## All Usage Flags

All of the original flags are preserved for full functionality.

*   `U`: An artist's SoundCloud username or a full URL for any supported site.
*   `-h`, `--help`: Show the help message and exit.
*   `-n NUM_TRACKS`, `--num-tracks NUM_TRACKS`: The number of tracks to download.
*   `-g`, `--group`: Use if downloading tracks from a SoundCloud group.
*   `-b`, `--bandcamp`: Use if downloading from Bandcamp rather than SoundCloud.
*   `-m`, `--mixcloud`: Use if downloading from Mixcloud rather than SoundCloud.
*   `-a`, `--audiomack`: Use if downloading from Audiomack rather than SoundCloud.
*   `-c`, `--hive`: Use if downloading from Hive.co rather than SoundCloud.
*   `-l`, `--likes`: Download all of a user's Likes on SoundCloud.
*   `-L LOGIN`, `--login LOGIN`: Set login for MusicBed.
*   `-d`, `--downloadable`: Only fetch tracks with an official, high-quality download link.
*   `-t TRACK`, `--track TRACK`: The name of a specific track by an artist to download.
*   `-f`, `--folders`: Organize saved songs in folders by artists.
*   `-p PATH`, `--path PATH`: Set a directory path where downloads should be saved.
*   `-P PASSWORD`, `--password PASSWORD`: Set password for MusicBed.
*   `-o`, `--open`: Open downloaded files automatically after downloading.
*   `-k`, `--keep`: Keep 30-second preview tracks (SoundCloud).
*   `-v`, `--version`: Display the current version of SoundScrape.

## Examples by Platform

Sets
-------

Soundscrape can also download sets, but you have to include the full URL of the set you want to download:

```bash
uv run soundscrape https://soundcloud.com/vsauce-awesome/sets/awesome
```

Groups
--------

Soundscrape can also download tracks from SoundCloud groups with the *-g* argument.

```bash
uv run soundscrape chopped-and-screwed -gn 2
```

Tracks
--------

Soundscrape can also download specific tracks with *-t*:

```bash
uv run soundscrape foolsgoldrecs -t danny-brown-dip
```

or with just the straight URL:

```bash
uv run soundscrape https://soundcloud.com/foolsgoldrecs/danny-brown-dip
```

Likes
--------

Soundscrape can also download all of an Artist's Liked items with *-l*:

```bash
uv run soundscrape troyboi -l
```

or with just the straight URL:

```bash
uv run soundscrape https://soundcloud.com/troyboi/likes
```

High-Quality Downloads Only
--------

By default, SoundScrape will try to rip everything it can. However, if you only want to download tracks that have an official download available (which are typically at a higher-quality 320kbps bitrate), you can use the *-d* argument.

```bash
uv run soundscrape sly-dogg -d
```

Keep Preview Tracks
--------

By default, SoundScrape will skip the 30-second preview tracks that SoundCloud now provides. You can choose to keep these preview snippets with the *-k* argument.

```bash
uv run soundscrape chromeo -k
```

Groups
--------
To download from a group:

```bash
uv run soundscrape chopped-and-screwed -gn 2
```

Tracks
--------
To download a specific track:

```bash
uv run soundscrape foolsgoldrecs -t danny-brown-dip
```

or with just the straight URL:

```bash
uv run soundscrape https://soundcloud.com/foolsgoldrecs/danny-brown-dip
```

Likes
--------
To download all of an Artist's Liked items:

```bash
uv run soundscrape troyboi -l
```

or with just the straight URL:

```bash
uv run soundscrape https://soundcloud.com/troyboi/likes
```

High-Quality Downloads Only
--------
By default, SoundScrape will try to rip everything it can. However, if you only want to download tracks that have an official download available (which are typically at a higher-quality 320kbps bitrate), you can use the *-d* argument.

```bash
uv run soundscrape sly-dogg -d
```

Keep Preview Tracks
--------
By default, SoundScrape will skip the 30-second preview tracks that SoundCloud now provides. You can choose to keep these preview snippets with the *-k* argument.

```bash
uv run soundscrape chromeo -k
```

Folders
--------
By default, SoundScrape aims to act like _wget_, downloading in place in the current directory. With the *-f* argument, however, SoundScrape acts more like a download manager and sorts songs into the following format:

```
./ARTIST_NAME - ALBUM_NAME/SONG_NUMBER - SONG_TITLE.mp3
```

It will also skip previously downloaded tracks.

```bash
uv run soundscrape murdercitydevils -f
```

Bandcamp
--------
To download from a Bandcamp page:

```bash
uv run soundscrape warsaw -b -f
```

This also works for non-Bandcamp URLs that are hosted on Bandcamp:

```bash
uv run soundscrape -b http://music.monstercat.com/
```

Note that the full URL must be included.

Mixcloud
--------
To download a Mixcloud set:

```bash
uv run soundscrape https://www.mixcloud.com/DjMoneyJ/x-ecutioners-built-from-scratch/
```

To download all of a user's uploads (up to the `-n` limit):
```bash
uv run soundscrape https://www.mixcloud.com/corenewsuploads/
```

Audiomack
--------

Just for fun, SoundScrape can also download individual songs from Audiomack. Not that you'd ever want to.

```bash
uv run soundscrape -a http://www.audiomack.com/song/bottomfeedermusic/top-shottas
```

MusicBed
--------

For some strange reason, it also works for MusicBed.com. Thanks @brachna for this feature.

```bash
uv run soundscrape https://www.musicbed.com/albums/be-still/2828
```

Opening Files
--------

As a convenience method, SoundScrape can automatically _'open'_ files that it downloads. This uses your system's 'open' command for file associations.

```bash
uv run soundscrape lorn -of
```

Issues
-------

There's probably a lot more that can be done to improve this. Please file issues if you find them!
