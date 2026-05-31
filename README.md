# The Practical Guide to Managing a Music Library

![Status](https://img.shields.io/badge/status-active-success)
![Music Library](https://img.shields.io/badge/topic-music%20library-blue)
![Self Hosted](https://img.shields.io/badge/self--hosted-friendly-orange)
![License](https://img.shields.io/badge/license-MIT-blue)

A practical guide to building, organizing, tagging, backing up, and preserving a personal music library.

## Contents

- [Introduction](#introduction)
- [Chapter 1 – The Philosophy: Metadata First](#chapter-1--the-philosophy-metadata-first)
- [Chapter 2 – Configuring MusicBrainz Picard](#chapter-2--configuring-musicbrainz-picard)

# Introduction

Music libraries have never been easier to build and never harder to maintain.

Storage is cheap, music is available in countless formats, and modern software can stream a collection to virtually any device. Yet many people still struggle with the same problems: duplicate albums, inconsistent metadata, broken artwork, missing lyrics, albums split into multiple entries, and libraries that become increasingly difficult to manage as they grow.

This guide focuses on solving those problems.

It is intended for anyone who owns a collection of digital music files and wants to organize them in a clean, consistent, and maintainable way. Whether your collection contains a few hundred tracks or tens of thousands, the principles remain the same.

This guide does **not** explain how to obtain music. It assumes that you already have audio files and want to build a well-structured library from them. The source of those files is outside the scope of this document.

The goal is simple: transform a folder full of audio files into a collection that is properly tagged, easy to navigate, compatible with modern music servers and players, and resilient enough to remain organized for years.

The workflow described here is based on widely adopted tools and standards, with a particular focus on [MusicBrainz Picard](https://picard.musicbrainz.org/), ReplayGain, [Navidrome](https://www.navidrome.org/), and self-hosted music management. However, most of the concepts apply equally well regardless of the software you choose.

Before discussing software, folder structures, or streaming servers, it is important to understand a fundamental concept:

a music library is not built on folders.

A music library is built on metadata.

# Chapter 1 – The Philosophy: Metadata First

One of the most common mistakes made when building a music collection is focusing on folder names before focusing on metadata.

Many users spend hours manually renaming directories, moving files between folders, and maintaining increasingly complex folder structures. While a clean directory layout is useful, it is not what defines a music library.

Modern music players and music servers do not primarily read folder names. They read metadata.

Artist names, album titles, release dates, track numbers, disc numbers, album artists, genres, artwork, ReplayGain information, and lyrics are all stored inside the files themselves. These tags are what allow software to understand and organize your collection correctly.

A properly tagged library can survive being moved to a different drive, copied to another computer, imported into a new application, or served through a music server with minimal effort.

A poorly tagged library, on the other hand, remains problematic regardless of how carefully the folders are organized.

For this reason, metadata should always be considered the single source of truth.

A clean music library rests on four fundamental pillars:

* accurate metadata
* consistent artwork
* proper ReplayGain information
* predictable file and folder naming

Notice that folder structure comes last.

Folders are important, but they should be generated from metadata rather than maintained manually. Once metadata is accurate and consistent, tools such as MusicBrainz Picard can automatically create a logical and predictable directory structure.

This approach has several advantages:

* fewer duplicates
* more reliable album grouping
* better compatibility across applications
* easier migration between platforms
* less manual maintenance over time

When users encounter problems such as albums appearing multiple times in Navidrome, tracks disappearing from a release, or compilations being split incorrectly, the cause is almost always inconsistent metadata rather than an incorrect folder structure.

For that reason, every step described in the following chapters begins with the same principle:

fix the metadata first.

Everything else comes afterwards.

# Chapter 2 – Configuring MusicBrainz Picard

Once the principles described in the previous chapter are understood, it is time to configure the tool that will become the foundation of the entire workflow: MusicBrainz Picard.

Picard is a free and open-source music tagger built around the MusicBrainz database. It is available for Windows, macOS, and Linux, and installation is straightforward regardless of platform.

Download and installation instructions can be found on the official website:

https://picard.musicbrainz.org/

For the purposes of this guide, the default installation is sufficient. No special installation options are required.

Before tagging any music, however, it is worth spending a few minutes configuring Picard properly. A good initial configuration will save countless hours later and help maintain a consistent library over time.

## Genre Settings

Genres are one of the most debated topics in music library management.

Some users prefer highly specific classifications with multiple genres assigned to every release. Others prefer a simpler approach focused on broad categories such as Rock, Country, Pop, Jazz, Blues, or Classical.

This guide follows the second approach.

The goal is not to build an exhaustive music taxonomy, but to maintain genres that remain useful when browsing a collection.

Under:

Metadata → Genres

configure the following options:

* enable **Use genres from MusicBrainz**
* enable **Fall back to album artist's genres**
* disable **Use folksonomy tags as genre**
* set **Minimal genre usage** to 90%
* set **Maximum number of genres** to 1
* leave **Join multiple genres with** empty

With these settings, Picard will only assign genres that have broad consensus within the MusicBrainz database and will limit each release to a single primary genre.

![Genre Metadata settings](images/01-metadata-genres.png)

This produces cleaner and more predictable results than allowing multiple overlapping genres or community-created folksonomy tags.

The exact values are ultimately a matter of personal preference, but maintaining consistency across the entire collection is more important than choosing any particular genre strategy.

## Cover Art Settings

Album artwork plays an important role in modern music libraries.

Most music players and servers display artwork directly in the interface, and many users expect artwork to remain available regardless of which application is used.

For maximum compatibility, this guide recommends storing artwork both inside the audio files and as a separate image file.

Under:

Cover Art

configure the following options:

* enable **Embed cover images into tags**
* enable **Embed only a single front image**
* enable **Save cover images as separate files**
* set image filename to **cover**
* enable **Overwrite the file if it already exists**
* disable **Save only a single front image as separate file**
* disable **Always use the primary image type as the file name**

For cover art providers:

* leave **Cover Art Archive (Release)** enabled
* leave **Allowed Cover Art URLs** enabled
* leave **Cover Art Archive (Release Group)** enabled
* enable **Local Files**

![Cover Art settings](images/02-cover-art.png)

Then open:

Cover Art → Cover Art Archive

and set:

Only use images of the following size: Full size

![Cover Art Archive settings](images/03-cover-art-archive.png)

This configuration provides excellent compatibility across players, media servers, and mobile applications while preserving the highest-quality artwork available from the source.

The reasoning behind these choices will be discussed in greater detail in the chapter dedicated specifically to artwork management.

## File Naming and Library Structure

One of Picard's greatest strengths is its ability to automatically organize a music collection.

Instead of manually creating folders and renaming files, metadata can be used to generate a consistent structure automatically.

The structure used throughout this guide is:

```text
Artist/
└── Year - Album/
    ├── 01 - Track.flac
    ├── 02 - Track.flac
    └── cover.jpg
```

This layout is simple, readable, and compatible with virtually every music player and self-hosted music server.

To configure it, open:

File Naming

and enable:

* **Move files when saving**
* **Delete empty directories**
* **Rename files when saving**

Then choose the destination directory that will contain your music library.

Important:

When Picard saves files with these settings enabled, it moves them into the destination library. The audio itself is not modified, but the files will no longer remain in their original location.

For this reason, many users maintain a temporary "incoming" directory containing newly acquired music and use Picard to move completed releases into the main library.

![File Naming settings](images/04-file-naming.png)

Select:

Edit file naming script...

and use the following naming script:

```text
%artist%/%originalyear% - %album%/$num(%tracknumber%,2) - %title%
```

This script automatically creates artist folders, album folders prefixed with the original release year, and consistently numbered track names.

The result is a library that remains predictable and easy to browse even when it grows to tens of thousands of tracks.

![File Naming Script Editor settings](images/05-file-naming-script-editor.png)

Users interested in advanced naming rules can consult the official Picard scripting documentation:

https://picard-docs.musicbrainz.org/en/latest/config/options_filerenaming_editor.html

## Installing the ReplayGain Plugin

ReplayGain deserves its own chapter because it has a significant impact on listening experience.

For now, the goal is simply to configure Picard so that ReplayGain information can be calculated automatically during the tagging process.

Open:

Plugins

Locate:

ReplayGain 2.0

and install it.

Once enabled, a new configuration section called:

ReplayGain 2.0

will appear in the settings menu.

![Plugins](images/06-plugins.png)

Before continuing, install the external utility rsgain.

Installation instructions are available at:

https://github.com/complexlogic/rsgain

After installation, configure ReplayGain as follows:

* **Path to rsgain**: `rsgain`
* enable **Calculate album gain/peak**
* enable **Use true peak**
* disable **Write reference loudness tags**
* set **Target Loudness** to -18 LUFS
* set **Clipping Protection** to "Enabled for positive gain values only"
* set **Max Peak** to -1 dB
* set **Opus Files** to "Write standard ReplayGain tags"
* leave **Always reference Opus R128_*_GAIN tags to -23 LUFS** disabled

These values provide a practical balance between consistency and listening comfort.

![ReplayGain 2.0 settings](images/07-replaygain.png)

ReplayGain standards, loudness targets, clipping protection, and alternative configurations will be discussed in detail later in this guide.

## Additional Plugins

Picard supports a large collection of optional plugins that extend its functionality.

A complete list is available at:

https://picard.musicbrainz.org/plugins/

Most users can begin with the default installation and ReplayGain plugin alone. Additional plugins can be added later as specific needs arise.

At this stage, the objective is simply to establish a clean, reliable, and repeatable tagging workflow.

# Chapter 3 – Common Mistakes That Break a Music Library

A well-organized music library can remain reliable for years.

A poorly organized one becomes increasingly difficult to maintain as it grows.

Most library problems are not caused by software bugs. They are usually the result of inconsistent metadata, incomplete tagging, or small mistakes that accumulate over time.

This chapter covers some of the most common issues encountered when managing a music collection and explains how to avoid them.

## Mixing Different Releases of the Same Album

One of the most common causes of duplicate albums in Navidrome, Jellyfin, and other music servers is mixing tracks from different releases of the same album.

To understand why this happens, it is important to understand how MusicBrainz works.

When Picard identifies an album, it does not simply associate your files with an album title. It associates them with a specific release recorded in the MusicBrainz database.

A single album can have dozens of different releases.

For example:

* original CD release
* digital release
* vinyl release
* SACD release
* anniversary edition
* deluxe edition
* releases intended for different countries or markets

Each of these releases has its own entry in MusicBrainz and may contain slightly different metadata.

For this reason, selecting the correct release is an important step during the tagging process.

One useful way to verify a match is to compare track durations. If the lengths shown by MusicBrainz closely match the lengths of your files, there is a good chance you have selected the correct release.

This is only a guideline, not an absolute rule. Sometimes MusicBrainz may only contain a release that differs from the files you own. In those situations, you can manually adjust the metadata and, if appropriate, contribute a new release to the MusicBrainz database.

It is important to remember that selecting a release does not alter the audio itself.

If MusicBrainz indicates a track length of 2:58 while your file is 3:00 long, Picard will not modify or trim the audio. The duration is simply metadata used for identification and matching.

### How Duplicate Albums Appear

A common scenario looks like this:

1. a few tracks from an album are added to the library
2. Picard associates them with Release A
3. weeks or months later, additional tracks from the same album are added
4. Picard associates them with Release B
5. the files are saved

![Choosing a release in Picard](images/08-choosing-release-picard.png)

![Album split into multiple releases inside Picard](images/09-album-split-into-multiple-releases-inside-picard.png)

At first glance everything appears correct.

The folder structure may look perfectly organized.

All tracks may even be located inside the same album directory.

![Single album folder on disk](images/10-single-album-folder-on-disk.png)

However, the metadata now references two different MusicBrainz releases.

As a result, Navidrome, Jellyfin, and similar applications may display what appears to be two separate copies of the same album.

![Duplicate album displayed in Navidrome](images/11-duplicate-album-displayed-navidrome.png)

### How to Fix It

The easiest solution is to ensure that all tracks belonging to an album are tagged against the same release.

If an album already exists in your library:

1. load the existing album into Picard
2. Picard will place it directly in the right-hand pane because it is already tagged
3. drag the new tracks onto that existing release
4. save the files again

This ensures that all tracks share the same release metadata.

After adding or replacing tracks, remember to recalculate ReplayGain for the entire album before saving.

Once all tracks belong to the same release, the duplicate album problem usually disappears immediately after the music server refreshes its library.

## Consistency Matters More Than Perfection

Many users spend a great deal of time searching for the "perfect" metadata.

In practice, consistency is often more important than perfection.

Small differences that seem harmless to a human reader can create confusion for music players and music servers.

A library should follow the same conventions everywhere.

Choose a method and apply it consistently.

### Artist Names

Artist names should always be written the same way throughout the collection.

For example, an artist might appear in one release as:

```text
Reba McEntire
```

and in another as:

```text
Reba
```

Both may be technically correct depending on the release metadata, but mixing naming styles can make browsing less predictable and may fragment artist pages in some applications.

If you decide to standardize artist names, apply the same rule consistently across the entire library.

### Featuring Artists

Featuring credits are another common source of inconsistency.

Different releases may use:

```text
feat.
featuring
with
&
and
```

MusicBrainz generally handles these situations well, but differences still appear from time to time.

The important thing is not which style you choose.

The important thing is choosing one approach and using it consistently throughout the collection.

A consistent library is easier to browse, search, and maintain.

## Essential Metadata Fields

Not every metadata field is equally important.

Some tags are optional and largely cosmetic.

Others are fundamental for proper library organization.

If you only verify a handful of fields when reviewing an album, verify these.

### Title

The song title.

Every track should have a clear and accurate title.

### Artist

The performer of the track.

This field identifies who performs the song and is one of the primary fields used when browsing a collection.

### Album

The album to which the track belongs.

Every track belonging to the same album should use exactly the same album name.

Even small differences can cause albums to split unexpectedly.

### Album Artist

This is one of the most important fields in a music library.

For standard albums, Album Artist is usually the primary artist.

For compilations, soundtracks, and various-artists collections, Album Artist should typically be set to:

```text
Various Artists
```

All tracks belonging to the same release should share the same Album Artist value.

Incorrect or missing Album Artist tags are one of the most common causes of album fragmentation.

### Track Number

Tracks should always have track numbers.

Without them, music servers may sort songs alphabetically instead of in album order.

### Disc Number

For multi-disc releases, Disc Number is essential.

Without it, tracks from different discs may become mixed together or appear in the wrong order.

### Date Information

Dates are often overlooked but provide valuable context.

This guide recommends preserving:

* Original release year
* Release year
* Full release date when available

These fields become particularly useful when working with reissues, remasters, anniversary editions, and deluxe releases.

### Genre

Genres are optional compared to the fields above, but they remain useful for browsing and filtering a large collection.

Consistency is more important than complexity.

### Compilation Flag

Compilation albums deserve special attention.

If an album contains tracks by multiple artists, the compilation flag and Album Artist metadata help ensure that the release is displayed as a single album rather than being fragmented into separate artist entries.

## Trust the Metadata, Not the Folder Structure

One of the recurring themes throughout this guide is that folders can be misleading.

An album can appear perfectly organized on disk while still containing metadata inconsistencies that confuse every application reading it.

When troubleshooting a music library, always inspect the metadata first.

If something appears broken in Navidrome, Jellyfin, Foobar2000, MusicBee, or another player, the cause is far more likely to be found in the tags than in the directory structure.

Metadata remains the single source of truth.

# Chapter 4 – ReplayGain

One of the most valuable additions you can make to a music library is ReplayGain.

Many users discover it only after experiencing a common problem: some albums play much louder than others.

A modern pop release may sound extremely loud, while an older jazz recording or a classical album may require a significant volume increase. Constantly adjusting the volume between tracks, albums, or artists quickly becomes frustrating.

ReplayGain was created to solve this problem.

## What ReplayGain Is

ReplayGain is a loudness normalization system based on metadata.

It analyzes the perceived loudness of your music and writes information into the file tags that compatible players can use during playback.

The important detail is that ReplayGain does **not** modify the audio itself.

The music remains untouched.

ReplayGain simply tells the player:

> "When playing this track or album, increase or decrease the volume by this amount."

The decision is made during playback, not during scanning.

This makes ReplayGain completely reversible and safe to use.

If you remove the ReplayGain tags, the audio files return to behaving exactly as they did before.

## What ReplayGain Does Not Do

ReplayGain is often misunderstood.

It does not:

* re-encode audio
* compress dynamic range
* change audio quality
* modify waveforms
* permanently increase or decrease volume
* rewrite the audio stream

ReplayGain only stores instructions for compatible players.

Because of this, it can safely be applied multiple times without degrading audio quality.

## ReplayGain vs Destructive Normalization

Many audio editors offer some form of "normalization".

Traditional normalization permanently modifies the audio data itself.

For example, a file might be rewritten so that its loudest sample reaches a chosen target level.

ReplayGain works differently.

Instead of changing the audio, it stores metadata describing how much adjustment should occur during playback.

This distinction is extremely important.

With destructive normalization:

* the audio is modified
* reverting the operation may not be possible
* repeated processing can reduce quality

With ReplayGain:

* the audio remains untouched
* the operation is fully reversible
* files can be rescanned at any time
* different loudness targets can be tested later

For a long-term music library, ReplayGain is generally the preferred approach.

## Understanding the ReplayGain Tags

For FLAC files, ReplayGain information is usually stored in tags similar to the following:

| Tag                           | Example Value | Purpose                                              |
| ----------------------------- | ------------- | ---------------------------------------------------- |
| REPLAYGAIN_TRACK_GAIN         | -3.21 dB      | Adjustment applied to an individual track            |
| REPLAYGAIN_TRACK_PEAK         | 0.943211      | Highest detected peak in the track                   |
| REPLAYGAIN_ALBUM_GAIN         | -5.45 dB      | Adjustment applied when playing the album as a whole |
| REPLAYGAIN_ALBUM_PEAK         | 0.922110      | Highest peak found anywhere in the album             |
| REPLAYGAIN_REFERENCE_LOUDNESS | -18.00 LUFS   | Loudness target used during scanning                 |

The player reads these values and decides how much volume adjustment should be applied during playback.

The audio file itself remains unchanged.

## Track Gain vs Album Gain

ReplayGain calculations produce two different types of information.

### Track Gain

Track Gain treats every song independently.

The goal is to make all tracks play at roughly the same perceived loudness.

This works well for:

* playlists
* shuffle playback
* mixed collections
* radio-style listening

### Album Gain

Album Gain analyzes the entire album as a single unit.

Rather than making every song equally loud, it preserves the intended volume differences between tracks.

This is especially important for:

* concept albums
* live albums
* classical music
* soundtracks
* albums designed with deliberate loudness variations

Most music servers, including Navidrome, can use Album Gain when listening to a complete album and Track Gain when listening in shuffle mode.

For this reason, this guide recommends calculating both values.

## Sample Peak and True Peak

When ReplayGain scans audio, it must determine how close the music comes to clipping.

Two different approaches exist.

### Sample Peak

Sample Peak simply checks the highest digital sample present in the file.

It is very fast and has traditionally been used by many ReplayGain scanners.

### True Peak

True Peak goes a step further.

Instead of only examining stored samples, it estimates what happens between samples during digital-to-analog conversion.

This produces a more realistic measurement of potential clipping and usually reports slightly higher peak values.

The difference is often small, but True Peak provides a safer estimate and is generally recommended on modern hardware.

For this reason, this guide enables:

* Use True Peak

in both Picard and rsgain.

## Clipping Protection

Clipping protection is one of the most misunderstood ReplayGain options.

It does not create additional tags.

It does not modify audio.

Instead, it affects how ReplayGain values are calculated.

Consider a track that would require a positive gain adjustment to reach the target loudness.

If increasing the volume by that amount would push the signal beyond the maximum safe level, clipping protection reduces the calculated gain accordingly.

The result is simply reflected in the final ReplayGain values written to the file.

Nothing else changes.

For most music libraries, enabling clipping protection only for positive gain adjustments provides a sensible balance between safety and loudness consistency.

## Choosing a Loudness Target

One of the first questions users encounter is:

"What loudness target should I use?"

There is no universally correct answer.

Different standards use different reference levels.

### -23 LUFS

The EBU R128 broadcast standard uses:

```text
-23 LUFS
```

This is an excellent choice for television and radio broadcasting but tends to sound unnecessarily quiet in a personal music library.

### -18 LUFS

ReplayGain 2.0 commonly uses:

```text
-18 LUFS
```

This has become a practical standard for many self-hosted music collections.

It provides good consistency while minimizing the need for clipping protection.

### -16 LUFS

Apple Music targets approximately:

```text
-16 LUFS
```

Many listeners consider this a good compromise between loudness and headroom.

### Why This Guide Uses -18 LUFS

The settings recommended earlier in this guide use:

```text
-18 LUFS
```

because it represents a balanced middle ground.

It is widely supported, aligns with modern ReplayGain workflows, and works well across mixed collections containing both older and newer recordings.

Users should feel free to experiment.

One of ReplayGain's greatest strengths is that the library can always be rescanned later.

## Why Reference Loudness Tags Are Disabled

Some ReplayGain scanners can write:

```text
REPLAYGAIN_REFERENCE_LOUDNESS
```

This field records the loudness target used during scanning.

While useful for informational purposes, it is not part of the official ReplayGain 2.0 specification and is not required by most players.

For this reason, this guide leaves it disabled.

The effective playback level is determined by the ReplayGain values themselves rather than by this informational tag.

## Why Max Peak Is Set to -1 dB

This guide uses:

```text
Max Peak = -1 dB
```

together with True Peak analysis.

Leaving one decibel of headroom helps reduce the risk of clipping introduced by decoding, resampling, or format conversion.

A value of:

```text
0 dB
```

is more aggressive and leaves less safety margin.

The difference may be small, but -1 dB has become a common and sensible choice for long-term library management.

## Using ReplayGain in Picard

Once the ReplayGain plugin has been installed and configured, calculating ReplayGain becomes part of the normal tagging workflow.

After tagging an album:

1. select the album in Picard
2. right-click the album entry
3. open the Plugins menu
4. choose Calculate ReplayGain
5. start the calculation

![Calculate ReplayGain in Picard](images/12-calculate-replaygain-picard.png)

Picard will analyze the files and write the ReplayGain tags.

For most albums, the process takes only a few seconds.

When the calculation is complete, the files can be saved normally.

For best results, ReplayGain should be calculated only after all tracks belonging to the album have been added and tagged.

## Changing Your Mind Later

One of ReplayGain's greatest advantages is flexibility.

Nothing is permanent.

If you decide that:

* the target loudness is too low
* the target loudness is too high
* different clipping protection settings would work better
* you prefer another ReplayGain strategy

you can simply recalculate the tags.

For a single album, loading it into Picard and running ReplayGain again is usually sufficient.

For an entire library, rsgain provides a faster solution.

## Reprocessing an Entire Library with rsgain

For large collections, [rsgain](https://github.com/complexlogic/rsgain) can scan and update ReplayGain information directly from the command line.

The simplest approach is to use rsgain's Easy Mode:

```bash
rsgain easy /path/to/music-library
```

This scans the library and writes ReplayGain tags using the defaults chosen by the developer. These defaults are already very close to the settings recommended earlier in this guide and, for many users, Easy Mode is all that is needed.

If you want more control, you can create a preset and tell rsgain to use it:

```bash
rsgain easy -p my_preset /path/to/music-library
```

A preset allows all ReplayGain settings to be stored in a single configuration file.

The example below closely mirrors the ReplayGain settings configured earlier in Picard. In practice, the main reason for using this preset instead of the default Easy Mode settings is to set the maximum peak level to -1 dB.

Example:

```ini
[Global]
TagMode=i
Album=true
TargetLoudness=-18
ClipMode=p
MaxPeakLevel=-1.0
TruePeak=true
Lowercase=false
ID3v2Version=keep
OpusMode=d
PreserveMtimes=false
```

These values can be adjusted freely if you want to experiment with ReplayGain behavior. The rsgain documentation provides clear explanations of the available options and the reasoning behind them, making it easy to choose different loudness targets, clipping modes, or peak settings.

This approach is particularly useful when updating an existing collection after changing ReplayGain preferences.

Because the audio itself is never modified, the entire library can be rescanned as many times as necessary.

## Further Reading

ReplayGain is a mature and well-documented standard.

For readers interested in the technical details, the following resources are highly recommended:

* Hydrogenaudio ReplayGain Knowledgebase:
  https://wiki.hydrogenaudio.org/index.php?title=ReplayGain

* rsgain Design Philosophy:
  https://github.com/complexlogic/rsgain#design-philosophy

Understanding every technical detail is not necessary to benefit from ReplayGain.

The most important concept is simple:

ReplayGain does not change your music.

It changes how compatible players choose to play it.
