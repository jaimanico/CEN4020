# LocalShelf product backlog

Initial requirements pass for the CEN4020 term project. Drafted with a language model from my answer to the previous homework. Every item is still **proposed**: this is the first elicitation pass, not a design or a sprint plan.

**LocalShelf** is a desktop music library. I point it at folders of audio files I already have. It keeps a local catalogue so search stays quick once the collection is large, and it plays those files without an account.

## Problem

Spotify, Deezer, and Apple Music all get slow to look through once a library passes a few thousand tracks. In my experience that shows up around 3,000 songs. Keeping the files locally is the more dependable way to listen. This project is that local library, small enough to build in one term.

## Scope

In this pass, the product is:

- a desktop app for one person on one computer
- a catalogue built from folders of music files already on disk
- search, browsing, playback, and simple playlists that work offline

Out of scope for now: connecting to a streaming catalogue, downloading music, removing DRM, a phone app, accounts, and syncing across devices. Podcasts and video are out too.

## Assumptions and open questions

Assumptions for this pass:

- I already have the audio files, and the app only plays those files.
- Playback can use an existing audio library. Writing decoders is a different project.
- A track is identified by its file path. Moving a file looks like a removal plus an addition until a later pass decides otherwise.

Still open:

- Is a library of about 10,000 tracks the right size to aim at, or is my collection larger?
- Is the graded build Windows-only?
- Are MP3, FLAC, M4A, Ogg Vorbis, and WAV the formats that matter in my folders?

## How to read an item

| Field | Meaning |
| --- | --- |
| Type | Functional or non-functional |
| Priority | **Must** for the version this term is aiming at. **Should** if that set is in good shape. |
| Depends on | Other items that have to be in place before this one can be accepted. |

## Summary

| Id | Title | Type | Priority | Depends on |
| --- | --- | --- | --- | --- |
| [REQ-001](#req-001-choose-library-folders) | Choose library folders | Functional | Must | — |
| [REQ-002](#req-002-scan-folders-for-audio) | Scan folders for audio | Functional | Must | REQ-001 |
| [REQ-003](#req-003-save-the-catalogue-locally) | Save the catalogue locally | Functional | Must | REQ-002 |
| [REQ-004](#req-004-update-the-catalogue-on-rescan) | Update the catalogue on rescan | Functional | Must | REQ-002, REQ-003 |
| [REQ-005](#req-005-read-track-names-from-tags-or-filenames) | Read track names from tags or filenames | Functional | Must | REQ-002 |
| [REQ-006](#req-006-group-tracks-into-albums) | Group tracks into albums | Functional | Must | REQ-005 |
| [REQ-007](#req-007-search-while-typing) | Search while typing | Functional | Must | REQ-003, REQ-005 |
| [REQ-008](#req-008-browse-by-artist-and-album) | Browse by artist and album | Functional | Must | REQ-005, REQ-006 |
| [REQ-009](#req-009-sort-a-track-list) | Sort a track list | Functional | Should | REQ-005 |
| [REQ-010](#req-010-play-a-local-file) | Play a local file | Functional | Must | REQ-002 |
| [REQ-011](#req-011-show-what-is-playing) | Show what is playing | Functional | Should | REQ-005, REQ-010 |
| [REQ-012](#req-012-keep-a-play-queue) | Keep a play queue | Functional | Should | REQ-010 |
| [REQ-013](#req-013-store-playlists-locally) | Store playlists locally | Functional | Must | REQ-003 |
| [REQ-014](#req-014-edit-and-play-a-playlist) | Edit and play a playlist | Functional | Must | REQ-010, REQ-013 |
| [REQ-015](#req-015-work-offline-without-an-account) | Work offline, without an account | Non-functional | Must | REQ-003, REQ-010 |
| [REQ-016](#req-016-keep-the-library-usable-when-files-go-missing) | Keep the library usable when files go missing | Functional | Should | REQ-004, REQ-013 |

## Library intake

### REQ-001. Choose library folders

- **Type:** Functional
- **Priority:** Must
- **Depends on:** None

As someone with music already on disk, I want to choose the folders that hold it, so that the library is my files.

**Acceptance:** I can add more than one folder, remove one, and see the current list of folders.

### REQ-002. Scan folders for audio

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-001

As someone with a large folder of music, I want those folders scanned for audio files, so that I do not import songs one by one.

**Acceptance:** A scan picks up MP3, FLAC, M4A, Ogg Vorbis, and WAV files in nested folders. A file that cannot be read is skipped and reported, and the rest of the scan finishes.

### REQ-003. Save the catalogue locally

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-002

As someone reopening the app, I want the catalogue saved on this computer, so that a large library does not have to be scanned from scratch every launch.

**Acceptance:** After a finished scan, quitting and reopening shows the same tracks without scanning again.

### REQ-004. Update the catalogue on rescan

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-002, REQ-003

As someone who adds albums over time, I want a rescan to notice new, changed, and removed files, so that the catalogue follows the folders.

**Acceptance:** A new file becomes a track, a changed file is updated, and a file that is no longer at its path is marked missing.

## Metadata

### REQ-005. Read track names from tags or filenames

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-002

As someone browsing a large collection, I want each track to show a title, artist, album, year, genre, and duration, so that I can tell songs apart.

**Acceptance:** Those fields come from tags when the tags exist. When the title or artist tag is missing, the filename or a parent folder name is used instead. A missing tag does not fail the scan of that file.

### REQ-006. Group tracks into albums

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-005

As a listener, I want tracks that belong together to show up as one album, so that I can open a record instead of a flat list of files.

**Acceptance:** Tracks that share an album artist and album name are one album, ordered by disc and track number.

## Lookup

### REQ-007. Search while typing

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-003, REQ-005

As someone whose library is past a few thousand songs, I want matches to appear as I type a title, artist, album, or genre, so that finding a song stays quick.

**Acceptance:** Search is case-insensitive across those four fields, including names filled in by REQ-005. On a library of about 10,000 tracks, with the catalogue already loaded, the results update as the query changes and the app stays responsive. The number 10,000 is a proposed target, above the roughly 3,000 tracks where streaming apps already felt slow, and it can change after I measure a real folder.

### REQ-008. Browse by artist and album

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-005, REQ-006

As a listener, I want to open an artist and then an album, so that I can move through the collection when I already know what I want.

**Acceptance:** The library can be opened as artists, then that artist's albums, then the tracks in album order.

### REQ-009. Sort a track list

- **Type:** Functional
- **Priority:** Should
- **Depends on:** REQ-005

As a listener, I want to sort a long list by title, artist, album, or year, so that the order is predictable.

**Acceptance:** Each of those sort keys works in ascending and descending order.

## Playback

### REQ-010. Play a local file

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-002

As a listener, I want to play, pause, seek, and skip the file on disk, so that the library is something I can listen to.

**Acceptance:** Choosing a track plays that file. Pause returns to the same position. Next and previous move within the album, playlist, or result list I started from. A missing file does not play, and the app says so.

### REQ-011. Show what is playing

- **Type:** Functional
- **Priority:** Should
- **Depends on:** REQ-005, REQ-010

As a listener, I want the current title, artist, and album visible while a track plays, so that I can tell what I am hearing.

**Acceptance:** Those three fields and the elapsed time stay visible during playback.

### REQ-012. Keep a play queue

- **Type:** Functional
- **Priority:** Should
- **Depends on:** REQ-010

As a listener, I want to line up tracks from different albums, so that playback is not limited to one album.

**Acceptance:** I can add a track to the end of the queue, remove one, and playback continues to the next queued track when the current one ends.

## Playlists

### REQ-013. Store playlists locally

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-003

As someone organizing a large collection, I want playlists saved on this computer, so that the organization is not tied to a streaming account.

**Acceptance:** I can create, rename, and delete a playlist, and it is still there after a restart.

### REQ-014. Edit and play a playlist

- **Type:** Functional
- **Priority:** Must
- **Depends on:** REQ-010, REQ-013

As a listener, I want to put tracks in a playlist and play them in that order.

**Acceptance:** I can add, remove, and reorder tracks. Starting the playlist plays the saved order. Removing a track from a playlist leaves the file in the catalogue.

## Local behavior

### REQ-015. Work offline, without an account

- **Type:** Non-functional
- **Priority:** Must
- **Depends on:** REQ-003, REQ-010

The catalogue, search, browsing, and playback work with the network disconnected, and the app has no sign-in step.

**Acceptance:** With the network off, an existing library still opens, search still runs, and a local file still plays. Library contents and play history stay on the machine.

### REQ-016. Keep the library usable when files go missing

- **Type:** Functional
- **Priority:** Should
- **Depends on:** REQ-004, REQ-013

As someone whose files live on ordinary disks, I want a missing file called out, so that a moved folder does not look like a randomly broken library.

**Acceptance:** Missing tracks show up in one place and cannot be played. A playlist entry for a missing track stays in the playlist, labeled unavailable, and plays again if a later rescan finds the file at the same path.
