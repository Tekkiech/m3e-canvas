Please implement Navitune in the Material 3 Expressive design language. An Android music player for a self-hosted Navidrome server (the Subsonic / OpenSubsonic API) that looks and feels like ArchiveTune: Material 3 Expressive, colors taken from the playing song's artwork, a floating pill navigation bar with the mini player docked on it, and a cinematic full-screen player.
Target a portrait phone screen (412×892dp), supporting both light and dark mode and following the device's system setting.
Build it for Android, as a native app.
The layout below is a rough sketch that conveys intent, not a finished spec. Do not reproduce it as a static picture; build the complete, usable app that this kind of product is normally expected to be.

## Colors
Use dynamic color: on Android 12+ apply the scheme generated from the user's wallpaper (dynamicLightColorScheme / dynamicDarkColorScheme), and fall back to the colors below where it is unavailable.
The fallback theme is ArchiveTune coral. Set these on the Material 3 light and dark color schemes and reference every UI color through its role.
Light scheme:
- primary #B2273D / onPrimary #FFFFFF / primaryContainer #FDDADA / onPrimaryContainer #40010A
- secondary #7F5353 / secondaryContainer #FFDAD9 / onSecondaryContainer #341012 / tertiaryContainer #FFDEAA / onTertiaryContainer #241A03
- surface #FFF8F7 / surfaceContainerLow #FAF2F1 / surfaceContainer #F4ECEC / surfaceContainerHigh #EFE6E6 / surfaceContainerHighest #E9E1E0
- onSurface #201A1A / onSurfaceVariant #524343 / outline #847373 / outlineVariant #D5C2C2
- inverseSurface #352F2F / inverseOnSurface #F7EFEF / inversePrimary #FCB4B4
- error #B3261E / onError #FFFFFF / errorContainer #F9DEDC / onErrorContainer #410E0B
Dark scheme:
- primary #FCB4B4 / onPrimary #630C1C / primaryContainer #8C142B / onPrimaryContainer #FDDADA
- secondary #EEBAB9 / secondaryContainer #653B3C / onSecondaryContainer #FFDAD9 / tertiaryContainer #594317 / onTertiaryContainer #FFDEAA
- surface #181212 / surfaceContainerLow #201A1A / surfaceContainer #241E1E / surfaceContainerHigh #2F2928 / surfaceContainerHighest #3A3333
- onSurface #E9E1E0 / onSurfaceVariant #D5C2C2 / outline #9E8D8C / outlineVariant #524343
- inverseSurface #E9E1E0 / inverseOnSurface #352F2F / inversePrimary #B2273D
- error #F2B8B5 / onError #601410 / errorContainer #8C1D18 / onErrorContainer #F9DEDC

## Shape, type and motion
- Corners follow the M3 Expressive defaults (pill buttons, 20dp cards, 28dp dialogs).
- Use Roboto as the typeface. Headlines, button labels and tabs use the M3 Expressive emphasized typography (the heavier headlineMediumEmphasized and similar styles).
- Motion uses MotionScheme.expressive(): a light spring bounce on transitions and state changes.

## Layout
There are 11 screens: "Connect", "Home", "Home, scrolled", "Search", "Library", "Album", "Artist", "Now playing", "Queue", "Lyrics", "Settings".

First launch: sign in to a Navidrome server. The same form adds another server later from Settings. Everything sits in one centered column.
The "Connect" screen, from top to bottom (overlapping parts are called out as such):
- Near the top, centered: a 96×96dp image placeholder.
- In the middle, centered: bold text "Connect to Navidrome" at 28sp.
- In the middle, centered: text "Stream your own music server, anywhere." at 16sp.
- In the middle: an outlined text field labeled "Server URL" with a leading dns icon; supporting text "https://music.example.com or http://100.x.y.z:4533".
- In the middle: an outlined text field labeled "Username" with a leading person icon.
- In the middle: an outlined text field labeled "Password" with a leading password icon.
- In the middle: a filled button "Connect" with a login icon (364dp wide).
- In the middle, centered: a text button "Advanced options" with a tune icon.
- Near the bottom: text "Works with Navidrome and any OpenSubsonic server." at 14sp.

The main feed, one scrolling column (max 1200dp wide, centered on tablets). A tonal backdrop fades from primaryContainer at 30% through secondaryContainer at 14% to transparent over the top 430dp. Pull to refresh uses the M3 Expressive pull-to-refresh with the shape-morphing loading indicator. Sections sit 18dp apart; each header is titleLargeEmphasized with a trailing chevron that opens the full list.
The "Home" screen, from top to bottom (overlapping parts are called out as such):
- Near the top: a top app bar titled "Navitune" with settings on the right.
- Near the top: a chip group: "All" (selected), "Recently added", "Most played", "Random".
- Near the top, aligned left: bold text "Quick picks" at 22sp.
- In the middle: a hero carousel of 5 cards (300dp tall, each card with 16dp corners, scrolling sideways, card titles 1: "Starlight Drive", 2: "Paper Satellites", 3: "Glasshouse", 4: "Night Bus Home", 5: "Salt & Static").
- In the middle, aligned left: bold text "Keep listening" at 22sp.
- In the middle: a uncontained carousel of 6 cards (160dp tall, each card with 16dp corners, scrolling sideways, card titles 1: "Northern Lines", 2: "Harbor Lights", 3: "Soft Machines", 4: "Velvet Hours", 5: "Low Tide", 6: "Signal Fires").
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.
- Near the bottom: a navigation bar with 3 destinations: "Home" (home), "Search" (search), "Library" (library_music); the first one is selected.

Not a separate destination: the rest of the Home feed, reached by scrolling Home down. The floating top bar has slid away, leaving only its status-bar scrim.
The "Home, scrolled" screen, from top to bottom (overlapping parts are called out as such):
- Near the top, aligned left: bold text "Speed dial" at 22sp.
- Near the top, in one row from left to right: a 114×114dp image placeholder, a 114×114dp image placeholder, a 114×114dp image placeholder (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, in one row from left to right: a 114×114dp image placeholder, a 114×114dp image placeholder, a 114×114dp image placeholder (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, in one row from left to right: a 114×114dp image placeholder, a 114×114dp image placeholder, a 114×114dp image placeholder (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, aligned left: bold text "Forgotten favorites" at 22sp.
- In the middle: a list of 2 items, top to bottom: "Paper Satellites" with supporting text "The Quiet Coast • Harbor Lights", a leading album icon (no background circle), a trailing more_vert icon, on a surface background; "Glasshouse" with supporting text "Mira Vale • Soft Machines", a leading album icon (no background circle), a trailing more_vert icon, on a surface background.
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.
- Near the bottom: a navigation bar with 3 destinations: "Home" (home), "Search" (search), "Library" (library_music); the first one is selected.

Search the whole server. Typing waits 300ms, then calls search3 (20 artists, 20 albums, 50 songs) and replaces the idle content with a top result followed by Songs, Albums and Artists sections; the chips narrow the results to one type and page further with the offsets. Recent searches are stored locally.
The "Search" screen, from top to bottom (overlapping parts are called out as such):
- Near the top: a search bar with the placeholder "Search songs, albums, artists".
- Near the top: a chip group: "Songs" (selected), "Albums", "Artists", "Playlists".
- Near the top, aligned left: bold text "Recent searches" at 16sp.
- In the middle: a list of 3 items, top to bottom: "aurora fields", a leading history icon (no background circle), a trailing north_west icon, on a surface background; "night bus", a leading history icon (no background circle), a trailing north_west icon, on a surface background; "ambient", a leading history icon (no background circle), a trailing north_west icon, on a surface background.
- In the middle, aligned left: bold text "Browse genres" at 16sp.
- In the middle: a chip group: "Electronic", "Indie", "Jazz", "Ambient", "Hip-Hop".
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.
- Near the bottom: a navigation bar with 3 destinations: "Home" (home), "Search" (search), "Library" (library_music); "Search" is selected.

A horizontal pager of five pages driven by the chip row: Library (shown here), Playlists, Songs, Artists and Albums, which also swipe sideways. The other four pages are lists or two-column grids with a sort dropdown, a list/grid toggle and, on Playlists, a create button; they are fed by getPlaylists, search3 with an empty query, getArtists and getAlbumList2 type=alphabeticalByName. The top bar stays put on this screen.
The "Library" screen, from top to bottom (overlapping parts are called out as such):
- Near the top: a top app bar titled "Navitune" with settings on the right.
- Near the top: a chip group: "Library" (selected), "Playlists", "Songs", "Artists", "Albums".
- Near the top, in one row from left to right: a filled card (84dp tall) with the headline "Starred" and the body "248 songs", a filled card (84dp tall) with the headline "Downloaded" and the body "Available offline" (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, in one row from left to right: a filled card (84dp tall) with the headline "Most played" and the body "All time", a filled card (84dp tall) with the headline "Recently added" and the body "Newest albums" (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, aligned left: bold text "Recently played" at 22sp.
- In the middle: a uncontained carousel of 6 cards (130dp tall, each card with 16dp corners, scrolling sideways, card titles 1: "Northern Lines", 2: "Harbor Lights", 3: "Soft Machines", 4: "Velvet Hours", 5: "Low Tide", 6: "Signal Fires").
- In the middle, aligned left: bold text "Your playlists" at 22sp.
- In the middle: a list of 2 items, top to bottom: "Late night drive" with supporting text "32 songs • 2 h 4 min", a leading queue_music icon, a trailing more_vert icon, on a surface background; "Sunday morning" with supporting text "18 songs • 1 h 11 min", a leading queue_music icon, a trailing more_vert icon, on a surface background.
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.
- Near the bottom: a navigation bar with 3 destinations: "Home" (home), "Search" (search), "Library" (library_music); "Library" is selected.

Album detail (getAlbum). Playlists and genres reuse this layout. The hero artwork runs full-bleed behind the transparent top bar and the centered title block, fading through a gradient (black 42% at the top, surface 78% at 72% of its height, then solid surface); the hero is at least 560dp tall on phones and the content column is at most 720dp wide.
The "Album" screen, from top to bottom (overlapping parts are called out as such):
- In the middle: a 412×412dp image placeholder.
  - Inside the image, layered on top of it (the container is the background; positions are relative to it):
    - Near the top: a top app bar titled "Northern Lines" with a arrow_back icon button on the left and more_vert on the right.
    - Near the bottom, centered: bold text "Northern Lines" at 32sp.
    - Near the bottom, centered: text "Aurora Fields" at 16sp.
    - Near the bottom, centered: text "Album • 2023 • 11 songs • 46 min" at 14sp.
- In the middle, in one row from left to right: a tonal icon button with the download icon (52dp), a tonal icon button with the shuffle icon (52dp), a filled button "Play" with a play_arrow icon (104dp wide), a tonal icon button with the favorite icon (52dp), a tonal icon button with the playlist_add icon (52dp) (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle: a list of 3 items, top to bottom: "Starlight Drive" with supporting text "Aurora Fields • 3:48", a leading counter_1 icon (no background circle), a trailing more_vert icon, on a surface background; "Paper Lanterns" with supporting text "Aurora Fields • 4:12", a leading counter_2 icon (no background circle), a trailing more_vert icon, on a surface background; "Coastline" with supporting text "Aurora Fields • 3:05", a leading counter_3 icon (no background circle), a trailing more_vert icon, on a surface background.
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.

Artist detail (getArtist, getArtistInfo2), with the same hero treatment as the album. Below the top songs come Albums (a sideways row of 144dp covers, newest first), Appears on, Similar artists (96dp circular avatars from getArtistInfo2) and an About card with the biography that expands on tap.
The "Artist" screen, from top to bottom (overlapping parts are called out as such):
- In the middle: a 412×412dp image placeholder.
  - Inside the image, layered on top of it (the container is the background; positions are relative to it):
    - Near the top: a top app bar titled "Aurora Fields" with a arrow_back icon button on the left and more_vert on the right.
    - Near the bottom, centered: bold text "Aurora Fields" at 36sp.
    - Near the bottom, centered: text "8 albums • 96 songs" at 14sp.
- In the middle, centered, in one row from left to right: a tonal icon button with the radio icon (52dp), a tonal icon button with the shuffle icon (52dp), a filled button "Play" with a play_arrow icon (104dp wide), a tonal icon button with the favorite icon (52dp) (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, aligned left: bold text "Top songs" at 22sp.
- In the middle: a list of 3 items, top to bottom: "Starlight Drive" with supporting text "Northern Lines", a leading album icon (no background circle), a trailing more_vert icon, on a surface background; "Coastline" with supporting text "Northern Lines", a leading album icon (no background circle), a trailing more_vert icon, on a surface background; "Night Ferry" with supporting text "Harbor Lights", a leading album icon (no background circle), a trailing more_vert icon, on a surface background.
- Near the bottom: "Starlight Drive" with supporting text "Aurora Fields", a leading album icon, a trailing play_arrow icon, on a surfaceContainerHigh background.

The full player in the Cinematic design. It is a draggable bottom sheet that grows out of the mini player; dragging down, the chevron and back all collapse it. Content uses onBackground (white on the artwork-based backgrounds), and the play tile uses that color as its fill with the surface color for its icon. 32dp side padding.
The "Now playing" screen, from top to bottom (overlapping parts are called out as such):
- Near the top, centered, in one row from left to right: a text icon button with the keyboard_arrow_down icon (48dp), text "Playing from Northern Lines" at 14sp (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, centered: a 348×348dp image placeholder.
- In the middle, centered, in one row from left to right: bold text "Starlight Drive" at 22sp, a tonal icon button with the share icon (44dp), a tonal icon button with the favorite icon (44dp), a tonal icon button with the more_horiz icon (44dp) (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, aligned left: text "Aurora Fields" at 16sp.
- In the middle, centered: a slider (initial value 36%).
- In the middle, centered, in one row from left to right: text "1:24" at 12sp, text "3:48" at 12sp (keep them on the same line, vertically centered; never stack or wrap them).
- In the middle, in one row from left to right: a tonal icon button with the shuffle icon (40dp / M3 S), a tonal icon button with the skip_previous icon, a filled icon button with the pause icon (96dp / M3 L), a tonal icon button with the skip_next icon, a tonal icon button with the repeat icon (40dp / M3 S) (keep them on the same line, vertically centered; never stack or wrap them).
- Near the bottom, centered: text "FLAC • 24-bit • 96 kHz • 2,304 kbps" at 12sp.
- Near the bottom, centered, in one row from left to right: a tonal button "Queue" with a queue_music icon (140dp wide), a tonal icon button with the bedtime icon (48dp), a tonal button "Lyrics" with a lyrics icon (140dp wide) (keep them on the same line, vertically centered; never stack or wrap them).

The queue sheet over the player. Tapping a row jumps to it, dragging a row's handle reorders, swiping a row away removes it. The queue is saved to the server (savePlayQueue, debounced and on pause) and restored at launch with getPlayQueue, so another device can pick up where this one stopped.
The "Queue" screen, from top to bottom (overlapping parts are called out as such):
- In the middle: a 412×852dp bottom sheet with a drag handle at the top (background surfaceContainerLow, 28dp top corners).
  - Inside the bottom sheet, layered on top of it (the container is the background; positions are relative to it):
    - Near the top, aligned left: bold text "Up next" at 22sp.
    - Near the top, aligned left: text "Northern Lines • 11 songs" at 14sp.
    - In the middle: a list of 5 items, top to bottom: "Starlight Drive" with supporting text "Aurora Fields • 3:48", a leading equalizer icon (no background circle), a trailing drag_handle icon, on a secondaryContainer background; "Paper Lanterns" with supporting text "Aurora Fields • 4:12", a leading album icon (no background circle), a trailing drag_handle icon; "Coastline" with supporting text "Aurora Fields • 3:05", a leading album icon (no background circle), a trailing drag_handle icon; "Harbor Wind" with supporting text "The Quiet Coast • 5:01", a leading album icon (no background circle), a trailing drag_handle icon; "Night Ferry" with supporting text "The Quiet Coast • 3:37", a leading album icon (no background circle), a trailing drag_handle icon.
    - Near the bottom, centered: a standard floating toolbar with the icon buttons shuffle, repeat, playlist_add, clear_all.

Full-screen synced lyrics on the same background as the player. Lines come from getLyricsBySongId (the OpenSubsonic songLyrics extension) when the server offers it, else getLyrics by artist and title, else LRCLIB. The active line is ExtraBold at full strength and the others SemiBold at 42–52% with a slight blur; the list keeps the active line a third of the way down and springs to the next one. Tapping a line seeks there, and word-timed lyrics light up word by word.
The "Lyrics" screen, from top to bottom (overlapping parts are called out as such):
- Near the top, in one row from left to right: a text icon button with the keyboard_arrow_down icon (48dp), a 48×48dp image placeholder, bold text "Starlight Drive" at 16sp, a text icon button with the more_vert icon (48dp) (keep them on the same line, vertically centered; never stack or wrap them).
- Near the top: bold text "We left with the windows down" at 24sp.
- In the middle: bold text "Counting every headlight" at 28sp.
- In the middle: bold text "You drummed on the dashboard" at 24sp.
- In the middle: bold text "Humming songs we never knew" at 24sp.
- In the middle: bold text "The night was ours to borrow" at 24sp.
- Near the bottom, centered: a slider (initial value 36%).
- Near the bottom, centered, in one row from left to right: a tonal icon button with the skip_previous icon, a filled icon button with the pause icon, a tonal icon button with the skip_next icon (keep them on the same line, vertically centered; never stack or wrap them).

Settings home: a server card, then one segmented list of categories that each open their own page.
The "Settings" screen, from top to bottom (overlapping parts are called out as such):
- Near the top: a top app bar titled "Settings" with a arrow_back icon button on the left.
- Near the top: a filled card (88dp tall) on primaryContainer with the headline "music.example.com" and the body "Signed in as alex • Navidrome 0.56".
- In the middle: a list of 7 items, top to bottom: "Appearance" with supporting text "Theme, colors, player design", a leading palette icon, a trailing chevron_right icon; "Player & audio" with supporting text "Quality, ReplayGain, crossfade", a leading graphic_eq icon, a trailing chevron_right icon; "Lyrics" with supporting text "Sources, size, animation", a leading lyrics icon, a trailing chevron_right icon; "Storage & downloads" with supporting text "Offline music, cache size", a leading download icon, a trailing chevron_right icon; "Scrobbling" with supporting text "Navidrome, Last.fm, ListenBrainz", a leading history icon, a trailing chevron_right icon; "Backup & restore" with supporting text "Settings and servers", a leading settings_backup_restore icon, a trailing chevron_right icon; "About" with supporting text "Version, licenses", a leading info icon, a trailing chevron_right icon.

## Behavior and navigation
- The image is the app mark, drawn inside an M3 Expressive MaterialShapes.Sunny shape filled with primaryContainer.
- The "Password" text field masks what is typed and has a trailing visibility toggle.
- The "Connect" button opens the "Home" screen with a fade when tapped. It also normalizes the URL (adds https:// when no scheme is typed, strips a trailing slash and /app), calls ping.view with token auth, then getUser and getOpenSubsonicExtensions. On success it stores the server and opens Home; on failure it shows the Subsonic error (wrong credentials, unreachable host, TLS error) under the matching field. The button shows the shape-morphing loading indicator while it waits.
- The "Advanced options" button expands a section with custom HTTP headers sent on every request (for Cloudflare Access service tokens: CF-Access-Client-Id / CF-Access-Client-Secret), a 'legacy password auth' switch for servers that reject token auth, and a 'trust this self-signed certificate' switch.
- Tapping the settings icon button on the right of the "Navitune" top app bar opens the "Settings" screen with a slide in from the right.
- The "Navitune" top app bar is shared by Home, Search and Library. It is transparent and floats over the content with a vertical scrim (surface 95% to transparent); it slides away while scrolling down and comes back on the first scroll up. The title is a 35dp app mark followed by the app name in titleLarge Bold. Trailing actions are tonal icon buttons on surfaceContainerHighest at 48% opacity: History (opens recently played) then Settings.
- The "All" chip starts a row of filter chips on surfaceContainerHigh at 78%, selected on secondaryContainer. They swap the feed below for one album list: All (the mixed feed), Recently added (getAlbumList2 type=newest), Most played (frequent), Random (random).
- The carousel is the Quick picks row: an M3 HorizontalCenteredHeroCarousel of songs (332dp tall on phones, 356dp at 600dp+, 380dp at 840dp+; cards at most 440dp wide, 10dp apart). Each card is the album art full-bleed with 32dp corners, a 1dp outlineVariant border at 72%, and a black gradient (transparent at the top, 8% at the middle, 84% at the bottom) under the title in titleLargeEmphasized white and the artist in bodyLarge white at 78%. The card of the song that is playing shows a 36dp primary circle with a volume_up icon in its top-end corner. Tapping a card plays that song followed by an instant mix (getSimilarSongs2); tapping the playing card toggles pause; long-press opens the song menu. The songs come from the most-played and recently-played albums (getAlbumList2 type=frequent and type=recent), topped up with getRandomSongs.
- Tapping the "Northern Lines" destination of the carousel opens the "Album" screen with a slide in from the right.
- The carousel is the Keep listening shelf: recently played albums (getAlbumList2 type=recent) as a two-row horizontal grid of grid items: 128dp square artwork with 8dp corners, the title below in bodyLarge Bold and the artist in bodyMedium on secondary. Tapping one opens the album.
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped. It also represents the mini player, not a list row: 70dp tall, 388dp wide (max 420dp), on surfaceContainerHigh. Paired with the navigation bar it has 28dp top corners and 12dp bottom corners and sits 4dp above the bar; alone (on screens without the bar) all corners are 32dp. Leading: 42dp circular artwork with a 1dp outline border at 20%, ringed by a 52dp CircularWavyProgressIndicator showing the playback position (indeterminate while buffering). Middle: title in titleMediumEmphasized and artist in bodySmall, both one line with a marquee. Trailing: previous and next as 48dp standard icon buttons (20dp icons) around play/pause as a 48dp filled primary icon button (24dp icon); disabled buttons fade to 38%. Swipe it sideways to skip tracks, swipe up or tap to open the full player, which grows out of it as a draggable bottom sheet. It sits above the navigation bar on Home, Search and Library, and alone at the bottom of every other screen except the player, queue and lyrics.
- Tapping the "Search" destination of the navigation bar opens the "Search" screen with a fade.
- Tapping the "Library" destination of the navigation bar opens the "Library" screen with a fade.
- The navigation bar is a floating pill, not an edge-to-edge bar: the M3 Expressive ShortNavigationBar inside a surfaceContainer Surface 78dp tall, at most 420dp wide, 12dp from the sides and 10dp above the gesture area, with 32dp corners (12dp top corners while the mini player sits on it) and level 2 tonal and shadow elevation. Icons crossfade between outlined and filled when selected. Double-tapping Search focuses the search field.
- The image starts Speed dial: a 3×3 grid of square tiles for pinned albums, artists and playlists (long-press any of them and choose Pin to speed dial), paged sideways with dot indicators when there are more than nine. A tile has 24dp corners, the artwork full-bleed, and its name in labelLargeEmphasized white over an 86dp black gradient at the bottom; the playing tile grows to 32dp corners with a 3dp inverseOnSurface border. Pins are stored locally.
- The image is the Random tile: a shuffle icon on primaryContainer; it plays getRandomSongs.
- The "Paper Satellites" list item is a song row, the pattern every song list in the app follows: 56dp album art with 10dp corners where the sketch has an icon, the title in bodyLarge SemiBold, 'artist • album' in bodySmall, and a more_vert button that opens the song menu sheet (play next, add to queue, add to playlist, star, download, go to album, go to artist, share, details). Swipe a row right to play it next and left to add it to the queue. The playing row gets a secondaryContainer background with 12dp corners and animated bars over its art. Forgotten favorites lists starred songs (getStarred2) not played for 30 days or more, as a sideways-snapping grid four rows tall.
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped.
- Tapping the "Search" destination of the navigation bar opens the "Search" screen with a fade.
- Tapping the "Library" destination of the navigation bar opens the "Library" screen with a fade.
- The "aurora fields" list item runs the search when tapped; its trailing arrow copies the text into the field for editing, and long-press removes it from the history.
- The "Electronic" chip starts the genre chips: every genre from getGenres, sorted by song count, wrapping onto as many lines as needed (a FlowRow) instead of scrolling. A genre opens the Album layout listing its albums (getAlbumList2 type=byGenre), where Play shuffles getSongsByGenre.
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped.
- Tapping the "Home" destination of the navigation bar opens the "Home" screen with a fade.
- Tapping the "Library" destination of the navigation bar opens the "Library" screen with a fade.
- Tapping the settings icon button on the right of the "Navitune" top app bar opens the "Settings" screen with a slide in from the right.
- The "Library" chip starts a row of expressive tab chips, not filter chips: full pills with 18dp by 10dp padding and a 20dp icon before the label; the selected one fills with primary and onPrimary content, the others sit on surfaceVariant at 50% with onSurfaceVariant content; selection animates color and scale.
- The "Starred" card is the first of four shortcut cards in two equal columns: 26dp corners, surfaceContainer blended 6–8% with the card's accent (Starred error, Downloaded primary, Most played secondary, Recently added tertiary), a 32dp circular icon bubble at 10–16% of the accent with the 16dp icon in the accent, the title in titleSmall Bold and the count in bodySmall. Starred opens getStarred2 songs.
- The "Downloaded" card opens the albums and playlists saved for offline listening.
- The "Most played" card opens getAlbumList2 type=frequent.
- The "Recently added" card opens getAlbumList2 type=newest.
- Tapping the "Northern Lines" destination of the carousel opens the "Album" screen with a slide in from the right.
- The "Late night drive" list item opens the "Album" screen with a slide in from the right when tapped. It also shows the playlist in the Album layout (getPlaylist, with a 2×2 collage of its first covers as the hero), with drag-to-reorder and swipe-to-remove when you own it (updatePlaylist).
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped.
- Tapping the "Home" destination of the navigation bar opens the "Home" screen with a fade.
- Tapping the "Search" destination of the navigation bar opens the "Search" screen with a fade.
- The image is the hero artwork (getCoverArt at 1200px) with no corners, center-cropped.
- Tapping the arrow_back icon button on the left of the "Northern Lines" top app bar goes back to the previous screen (playing the entry transition in reverse).
- The "Northern Lines" top app bar stays transparent over the artwork and shows its title only after the hero has scrolled away, when it also takes the surface color. More opens the album menu: play next, add to queue, add to playlist, download, go to artist, share (createShare), details.
- The text is the title in headlineLarge; the artist line below is titleMedium at 82%, the details line bodyMedium at 76%.
- The text opens the "Artist" screen with a slide in from the right when tapped.
- The icon button downloads every track for offline play, turning into a circular progress ring while it runs and a check when done. The four round action buttons are 52dp FilledTonalIconButtons on the content color at 16%, balanced two on each side of Play.
- The icon button shuffles the album.
- The "Play" button is a medium (56dp) pill that plays from the first track.
- The icon button is a toggle button that flips on / off with every tap (when on, the style becomes filled). It also stars the album on the server (star / unstar with albumId); while starred it turns error at 16%.
- The icon button adds the whole album to a playlist.
- The "Starlight Drive" list item is a track row: the track number replaces the album art, and a 'Disc 2' header separates discs on multi-disc albums.
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped.
- The image is the artist image from getArtistInfo2 (largeImageUrl), falling back to the newest album's cover.
- Tapping the arrow_back icon button on the left of the "Aurora Fields" top app bar goes back to the previous screen (playing the entry transition in reverse).
- The icon button starts an artist radio: getSimilarSongs2 with the artist id.
- The icon button is a toggle button that flips on / off with every tap (when on, the style becomes filled). It also stars the artist.
- The "Starlight Drive" list item lists getTopSongs for the artist, falling back to the artist's songs sorted by play count when the server has no Last.fm data.
- The "Starlight Drive" list item opens the "Now playing" screen with a slide up from the bottom when tapped.
- The icon button goes back to the previous screen (playing the entry transition in reverse) when tapped.
- The image is the artwork with 16dp corners (adjustable in Appearance). Swipe it sideways to skip; double-tap its left or right half to seek 10s.
- The text is the title in titleLarge Bold on one line with a marquee; the artist line under it and the title form one column that fills the row, with the three action tiles at its end. Tapping the title opens the album; long-press copies it.
- The text opens the "Artist" screen with a slide in from the right when tapped.
- The icon button is the first of three 44dp rounded-square tiles (14dp corners) on the content color at 12%. It shares a Navidrome share link (createShare), or the text 'Title – Artist' when sharing is off on the server.
- The icon button is a toggle button that flips on / off with every tap (when on, the style becomes filled). It also stars the song; while starred the tile turns error at 25% with an error-colored heart.
- The icon button opens the player menu: add to playlist, go to album, go to artist, playback speed and pitch, equalizer, details (codec, bitrate, sample rate, file path).
- The slider is the seek bar in the content color, with the elapsed and total time under its ends in labelMedium. Its look is a setting: Standard, Wavy (squiggles while playing), Thick, Circular or Simple.
- The icon button is drawn, like repeat, as a 46dp rounded square (16dp corners) on the content color at 8%, rising to 20% with a full-strength icon when on; repeat cycles off, all and one.
- The icon button is drawn, like next, as a 56dp rounded square (18dp corners) on the content color at 15% with a 28dp icon.
- The icon button is an 88dp play/pause tile whose corners spring between 44dp (a circle, while paused) and 28dp (a squircle, while playing) with a medium-bouncy spring, holding a 44dp icon, or a 40dp CircularWavyProgressIndicator while buffering. The side controls scale down together on narrow screens.
- The text is the codec line built from the song's suffix, bitDepth, samplingRate and bitRate; it reads 'Transcoded to OPUS • 192 kbps' when the stream is transcoded.
- The "Queue" button opens the "Queue" screen with a slide up from the bottom when tapped. It also is, like Lyrics, a 16dp-cornered tile on the content color at 10% rather than a pill.
- The icon button sets the sleep timer (minutes, or end of the current song); while it runs the button shows the time left and a tap cancels it.
- The "Lyrics" button opens the "Lyrics" screen with a fade when tapped.
- The "Starlight Drive" list item is the current song, on secondaryContainer with 12dp corners and animated bars over its art.
- The toolbar reshuffles what is left, cycles repeat, saves the queue as a playlist (createPlaylist) and clears the queue (with an undo snackbar).
- The icon button goes back to the previous screen (playing the entry transition in reverse) when tapped.
- The image is the small artwork, 10dp corners.
- The text has the artist under it in bodyMedium.
- The icon button opens the lyrics menu: text size, sync offset in 0.5s steps, provider, and share as an image card.
- The text is the active line.
- Tapping the arrow_back icon button on the left of the "Settings" top app bar goes back to the previous screen (playing the entry transition in reverse).
- The "music.example.com" card shows the user's avatar (getAvatar) in a circle on onPrimaryContainer at 12%, the server host in titleMedium, the user and server version in bodyMedium at 70% and a chevron at the end. It opens the server list to switch servers, add one (the Connect form) or sign out.
- The "Appearance" list item is the first category row: 88dp tall, 22dp by 14dp padding, a 52dp circular icon bubble filled with the row's accent (primary, secondary or tertiary in turn) and the icon in its on-color, the title in titleMedium and the subtitle in bodyMedium on onSurfaceVariant, on surfaceContainerLow. The group has 28dp outer and 6dp inner corners, and rows press-scale to 97%.
- The "Now playing" screen opens the "Queue" screen with a slide up from the bottom when swiping up; the screen follows the finger while dragging.

## Component styles
Per-component guidance for the parts in use. The numbers are the M3 Expressive defaults: let the standard components handle whatever they already do, and adjust where the content calls for it.
- Images: 20dp corners; a surfaceContainerHighest placeholder when none is provided. Keep the aspect ratio and center-crop.
- Text: the specified sp size; headings on onSurface, descriptions on onSurfaceVariant, line height 1.3–1.5× the size. No ripple or press feedback on tap.
- Text fields: 56dp tall. Outlined has 16dp corners and an outline border; filled sits on surfaceContainerHighest with an underline. On focus the label floats up and the border becomes 2dp primary. Supporting text goes underneath in bodySmall.
- Buttons: medium size, 56dp tall, fully rounded (pill). Filled uses primary, tonal uses secondaryContainer, outlined has a 1dp outline border. A connected button group is a row with 3dp gaps where only the inner adjoining corners shrink to 8dp and the outer corners stay round (the M3 Expressive connected button group). A button given a height follows the M3 size scale (XS 32dp, S 40dp, M 56dp, L 96dp, XL 136dp): take the side padding, the label size and the icon size of that size, and keep the corner radius at half the height.
- Top app bar: 64dp tall on surface, with its background extended behind the status bar (pad the top by the system inset). Title in titleLarge, 48dp icon buttons on each side. A bar named medium or large is M3's flexible top app bar: 112dp or 152dp tall, the icons in the top 64dp row and the title on its own line at the foot (headlineSmall / headlineMedium), collapsing to the small bar on scroll. The standard tint to surfaceContainer on scroll is fine.
- Chips: 32dp tall by default, with 8dp corners. A chip given a height follows the M3 size scale (XS 32dp, S 40dp, M 56dp): take the side padding, the label size and the icon size of that size. The selected state fills with secondaryContainer and shows a leading check icon. A connected chip group is a row with 3dp gaps where only the inner adjoining corners shrink to 4dp, the outer corners stay round, and every chip shares one height; it scrolls horizontally when it overflows.
- Carousel: the M3 Carousel (HorizontalMultiBrowseCarousel / HorizontalUncontainedCarousel in Compose; a sideways-scrolling row of cards on the web). Cards are containers with 16dp corners; multi-browse and hero show the first card large and the rest smaller, uncontained shows every card at one width, full-screen gives one card the row. It runs edge to edge with a 16dp start margin and 8dp between cards. A card's title sits along its bottom edge.
- List items: 72dp tall, 24dp leading icon (on a 40dp primaryContainer circle unless stated), headline in bodyLarge, supporting text in bodyMedium on onSurfaceVariant, on the specified background role (surfaceContainerLow unless stated). A stacked list is a vertical run with 3dp gaps, 28dp outer corners and 8dp inner corners (the M3 Expressive list treatment).
- Navigation bar: 80dp tall on surfaceContainer, with its background extended down through the gesture navigation area (pad the bottom by the system inset). The active destination shows a secondaryContainer pill indicator (64×32dp), a filled icon and a labelMedium label.
- Search bar: 56dp tall, fully rounded, on surfaceContainerHigh (an outlined one sits on surface with an outline border), with a leading search icon and the specified trailing icon.
- Cards: 20dp corners. Place each card's image area where its line says — on top, along the bottom, filling the leading or trailing side, or as a full-bleed background (a scrim fades in from the text's side: dark under light text, light under dark text). Images keep their aspect ratio and are center-cropped to fill their area. Filled uses surfaceContainerHighest, elevated uses surfaceContainerLow with a level 1 shadow, outlined has a 1dp outlineVariant border. Headline in titleMedium, body in bodyMedium. 20dp padding, 4dp between headline and body, 12dp between the image and the text.
- Icon buttons: 56dp circles by default (M3's medium size); one given a size follows the M3 size scale (XS 32dp, S 40dp, M 56dp, L 96dp, XL 136dp), with the icon of that size. Filled / tonal / outlined / standard as specified. A connected run of icon buttons is a connected button group.
- Sliders: the M3 Expressive thick track (16dp) with a tall handle (4×44dp). Primary on the left of the handle, secondaryContainer on the right. Dragging changes the value.
- Bottom sheets: modal bottom sheets that slide up from the bottom edge, with a drag handle centered at the top, the specified background token and top corner radius; the bottom corners stay square.
- Floating toolbar: the M3 Expressive HorizontalFloatingToolbar. 64dp tall, fully rounded, floating 16dp above the bottom edge over the content. Standard uses surfaceContainer, vibrant uses primaryContainer. The icon buttons inside are 48dp.

## General guidance
- Work out what kind of app this is from the purpose of the screens, and implement the features such an app is normally expected to have (create, list, detail, edit, delete, search, settings, whichever apply) even where the sketch does not show them.
- Treat the data as real. Persist what the user creates on the device (Room, DataStore or similar) so it survives restarts. Do not ship dummy or sample data; show an empty state when there is nothing yet. Validate input, and confirm or report failures and deletions appropriately.
- Fill in behavior the sketch leaves out from the purpose of the screen and the labels of the parts. A button or item with no behavior specified should do what its label implies (save, send, open a detail screen, and so on), never nothing.
- The layout only needs to keep the intent (order, grouping, relative placement); sizes and spacing may be adjusted to fit the content. If something would break on a device, prefer working over matching the sketch.
- Use the standard components from Jetpack Compose material3 (latest, including the Expressive APIs); do not custom-draw parts the library provides.
- Always reference colors through the scheme roles above (primary, surfaceContainer, …) instead of hard-coded values.
- Keep 16dp screen margins and 8–16dp between parts, and use the M3 type styles (titleLarge, bodyMedium, …).
- Parts described as "in one row" must share a single Row (horizontal container) on the same line; never stack them vertically or wrap them. The row is as tall as its tallest part and the others are vertically centered in it.
- Parts described as "layered inside" a container are drawn on top of that container (a Box with the container as its background). The overlap is intentional: do not separate or reorder them for layout reasons. Later items in the description are drawn in front of earlier ones.
- Give every tappable part ripple plus a slight press-scale. "Back" plays the entry transition in reverse, and the system back gesture / button must do the same.
- Use Material Symbols Rounded for icons.
- Write unit tests for the main logic and hand it over with all of them passing.
- Keep the main features usable without a network, syncing when it returns if needed.

---

Everything above this line was generated by M3E Canvas from the sketch. Everything below comes from reading ArchiveTune's source and the Subsonic / OpenSubsonic API. Where the two disagree, and in particular where the generic "Component styles" above disagree with the notes on a part or with this section, this section and the part notes win.

## What this app is

Navitune is a native Android client for a self-hosted Navidrome server. It is built from scratch, but it should be hard to tell it apart from ArchiveTune (github.com/Tekkiech/archivetuneapp, a fork of rukamori/ArchiveTune): the same Material 3 Expressive look, spacing, motion and player. The music comes only from the user's Navidrome server through the Subsonic API with the OpenSubsonic extensions. There is no YouTube, no Google sign-in and no bundled sample data. The track and artist names in the sketch are placeholders that show where real data goes.

ArchiveTune's source is the visual reference. When a detail here is ambiguous, open the matching file under `app/src/main/kotlin/moe/rukamori/archivetune/` and match what it draws:

| What | File |
|---|---|
| Theme, seed color, pure black | `ui/theme/Theme.kt`, `ui/theme/Type.kt` |
| Artwork colors, player backgrounds | `ui/theme/PlayerColorExtractor.kt`, `ui/theme/PlayerBackgroundColorUtils.kt`, `ui/player/PlayerComponents.kt` (search `PlayerBackgroundStyle.`) |
| Sizes | `constants/Dimensions.kt` |
| Floating header, top bar buttons | `MainActivity.kt` (`TranslucentTopAppBarIconButton`, the floating `TopAppBar`) |
| Floating navigation bar | `ui/component/FloatingNavigationToolbar.kt` |
| Mini player | `ui/player/MiniPlayer.kt`, `ui/player/MiniPlayerComponents.kt` |
| Cinematic player (`PlayerDesignStyle.V4`) | `ui/player/Player.kt`, `ui/player/PlayerComponents.kt`, `ui/player/Thumbnail.kt`, `ui/player/QueueComponents.kt` (`QueueCollapsedContentV4`) |
| Lyrics | `ui/component/LyricsV2.kt`, `ui/player/LyricsScreen.kt` |
| Home sections | `ui/screens/HomeScreen.kt`, `ui/screens/HomeScreenComponents.kt`, `ui/component/SpeedDialGridItem.kt` |
| Library tab chips, shortcut cards | `ui/screens/library/LibraryScreen.kt` (`ExpressiveTabChip`), `ui/screens/library/LibraryMixScreen.kt` (`ShortcutCard`) |
| Album / artist hero | `ui/component/MediaDetailHero.kt`, `ui/screens/AlbumScreen.kt`, `ui/screens/artist/ArtistScreen.kt` |
| Rows, grid items, swipe actions | `ui/component/Items.kt` (`ListItem`, `GridItem`, `SwipeToSongBox`) |
| Settings rows | `ui/screens/settings/SettingsComponents.kt` (`SettingsSegmentedItem`) |

Licensing: ArchiveTune is GPL-3.0. License Navitune under GPL-3.0 too, so porting a composable from it is allowed. Keep the original copyright header on any file you port, and credit ArchiveTune in About. Do not use the ArchiveTune name, logo, app icon or other branding, which its license notice reserves. Navitune needs its own icon: a simple mark on a coral background works.

## Visual system (overrides the sketch where they differ)

- **Typeface:** Poppins (Google Fonts, OFL) is the app font across the whole M3 type scale, at the standard M3 sizes. It replaces the Roboto named above. Lyrics use a heavy display face. ArchiveTune bundles SF Pro Display Bold, but Apple's license does not allow that, so use Inter Display Bold / ExtraBold (OFL) instead. Appearance offers Default (Poppins), System and Custom (a .ttf/.otf the user picks through the Storage Access Framework).
- **Shapes:** `MaterialExpressiveTheme` with `Shapes(extraSmall = 8.dp, small = 12.dp, medium = 16.dp, large = 24.dp, extraLarge = 32.dp)`. List artwork: 56dp with 10dp corners. Grid artwork: 128dp (104dp in the small grid size) with 8dp corners. Album covers in rows: 144dp.
- **Motion:** `MotionScheme.expressive()`. Every color role animates with `animateColorAsState` and the scheme's default effects spec whenever the scheme changes. A "Disable animations" setting swaps in a motion scheme whose specs are all `snap()`.
- **Color, as ArchiveTune does it:**
  1. "Dynamic theme" is on by default. Whenever the current song changes, load its cover at a small size (Coil, `allowHardware(false)`) and pick a seed with `androidx.palette` (max 16 colors). Take the first swatch that exists, in this order: vibrant, dominant, muted, light vibrant, dark vibrant, light muted, dark muted. Rebuild the whole scheme from that seed with MaterialKolor (`com.materialkolor:material-kolor`, `dynamicColorScheme(seedColor, isDark, style)`). The style is `TonalSpot`, or `Neutral` when the seed's HCT chroma is below 12, or `Monochrome` below 4. The change animates as described under Motion.
  2. With nothing playing: on Android 12+ use the system dynamic colors (wallpaper), otherwise a seed taken the same way from the wallpaper bitmap, falling back to coral `#ED5564`.
  3. With dynamic theme off: the user's chosen seed (a palette picker with presets; the default is coral `#ED5564`) goes through the same MaterialKolor path. The coral scheme printed above is what this produces.
  4. "Pure black" (dark mode only) turns surface, background and every surfaceContainer role to `#000000`, and the nav, mini player and top bar follow.
- **Player background** (Appearance). With Default, content is onBackground on surface. With every other style, content is white and the play icon black. The artwork palette is up to six distinct, slightly saturated swatches, ranked by population and vividness. Greyscale art gets a ramp of greys instead, and missing colors are made by hue-shifting the seed.
  - Default: the theme surface.
  - Gradient: vertical, color 1 at 92%, color 2 at 75% (at 50%), color 3 at 65%, plus a black 18% overlay.
  - Blur: the artwork cropped to fill and blurred (`Modifier.blur` / RenderEffect on API 31+, a downscaled pre-blurred bitmap below that). Over it, a gradient of the artwork colors (45%, 38%, 35%, 50% at 0 / 0.4 / 0.75 / 1) and black at 8%.
  - Blur gradient: the blurred art under color stops of 55%, 48%, 42%, 38% and 35% at 0 / 0.2 / 0.5 / 0.8 / 1, plus black at 5%.
  - Coloring: one artwork color, clamped to HSV value 0.18–0.5, fading to 82% and then 60% of its brightness and on to black at 88%, plus black at 25%.
  - Glow: a black base with four radial glows (start, end, top and bottom), plus black at 24%.
  - Animated glow: the same glows drifting slowly.
  - Custom: a user-picked image with blur and dim sliders.
- **Mini player background** (Appearance): Theme (surfaceContainerHigh), Gradient or Glow, using the same recipes. On the artwork styles the title is white, the artist white at 72%, the progress white on a white 24% track, play a white 92% tile with a black icon, and previous / next sit on black at 22%.
- **Player design:** build Cinematic (the sketch) as the only design, behind a `PlayerDesign` enum so ArchiveTune's other layouts (Classic, Modern, Minimal, Little, Expressive, Immersive, Editorial) can be added later.
- **Menus:** long-press on any song, album, artist or playlist, or its more button, opens a `ModalBottomSheet` menu. The header shows the 56dp art, the title and subtitle, and a star toggle. Under it is a grid of large tonal actions (Play next, Add to queue, Add to playlist, Share), then a list (Start radio, Download, Pin to speed dial, Go to album, Go to artist, Details).
- **Loading and empty states:** use shimmer placeholders shaped like the real rows and tiles while a screen loads its first page, the M3 Expressive `LoadingIndicator` for paging and pull-to-refresh, and an illustrated empty state with one action ("Retry", "Browse your library") when there is nothing to show. While the server cannot be reached, a network banner slides down under the top bar ("Offline – showing downloads").
- **Haptics:** a `CONTEXT_CLICK` on the transport buttons and a long-press tick on menus, with a setting to turn them off.
- **Adaptive layout:** edge-to-edge, predictive back. From 600dp wide, the floating nav becomes a `NavigationRail` on surfaceContainer and the feed centers at max 1200dp. The player puts the artwork and the controls side by side in landscape.

## Navidrome / Subsonic data layer

- **Requests:** `GET {base}/rest/{method}?u={user}&t={token}&s={salt}&v=1.16.1&c=Navitune&f=json`. Make a fresh random salt (12+ hex characters) for each request, with `t = md5(password + salt)` in lowercase hex. Behind the "legacy password auth" switch, send `p=enc:{hex(password)}` instead. Parse the `subsonic-response` envelope (`status`, `version`, `serverVersion`, `openSubsonic`, `error.code`, `error.message`) with kotlinx.serialization (`ignoreUnknownKeys = true`), and turn error codes into typed errors: 40 wrong credentials, 50 not authorized, 70 not found.
- **At connect:** call `getOpenSubsonicExtensions` and remember which extensions exist (`songLyrics`, `transcodeOffset`, `formPost`, …). Gate features on that list, never on the server name. Also call `getMusicFolders` and offer a folder filter in Settings.
- **One OkHttpClient** feeds the API client (Ktor with the OkHttp engine, as ArchiveTune does), Coil 3 (`coil-network-okhttp`) and Media3 (`OkHttpDataSource`). One interceptor adds the auth parameters and the server's custom headers, so Cloudflare Access `CF-Access-Client-Id` / `CF-Access-Client-Secret` reach images and audio streams as well as API calls.
- **Stable cache keys:** the salt changes on every request, so URLs never repeat. Give Coil explicit memory and disk cache keys (`cover:{coverArtId}:{size}`), and give Media3 a `CacheKeyFactory` keyed on `{songId}:{format}:{maxBitRate}`. Without this, every image and song is downloaded again each time.
- **Transport security:** the network security config allows cleartext (LAN and Tailscale servers like `http://100.x.y.z:4533` are common) and trusts user-installed CAs. The Connect screen warns when a plain-http URL points at a public address. "Trust this self-signed certificate" pins that host's certificate SHA-256 in a per-host TrustManager, never trust-all. The password is encrypted with an Android Keystore AES-GCM key (or Tink) and stored as ciphertext in DataStore. It never appears in logs, crash reports or backups.
- **Endpoints by feature:**
  - Home: `getAlbumList2` (`recent`, `frequent`, `newest`, `random`, `starred`, `byGenre`), `getRandomSongs` and `getStarred2`.
  - Library: `getArtists`, `getPlaylists`, and `search3` with `query=""` paged through `songOffset` for all songs. `getAlbumList2 alphabeticalByName` pages 100 at a time with Paging 3.
  - Detail: `getAlbum`, `getAlbumInfo2`, `getArtist`, `getArtistInfo2`, `getTopSongs` (it takes the artist **name**, `count=10`), `getSimilarSongs2`. When similar songs come back empty (no Last.fm agent on the server), fall back to random songs of the same genre.
  - Search: `search3`, genres (`getGenres`, `getSongsByGenre`).
  - Playlists: `createPlaylist`, `updatePlaylist` (`songIdToAdd`, `songIndexToRemove`, name), `deletePlaylist`.
  - Annotations: `star` / `unstar` (`id`, `albumId`, `artistId`) and `setRating` (a 5-star row in Details).
  - Plays: `scrobble` with `submission=false` when a track starts (now playing) and `submission=true` once 50% or 4 minutes have played. Navidrome forwards plays to Last.fm and ListenBrainz when the user has linked them in Navidrome, so do not build those clients.
  - Media: `stream` (`maxBitRate`, `format`, plus `timeOffset` when `transcodeOffset` exists), `download` (the original file, for offline), `getCoverArt` (`size`), `getLyricsBySongId` (when `songLyrics` exists), `getLyrics`, and `getAvatar` (show initials if it fails).
  - Queue sync: `getPlayQueue` and `savePlayQueue` (`id`s, `current`, `position`).
  - Sharing: `createShare`.
  - Admins: `getScanStatus` / `startScan` under Settings, Server.
- **Local data:** Room caches everything browsed (artists, albums, songs, playlists, lyrics, play queue) so screens open instantly and work offline. Show cached data first, refresh in the background, and let pull-to-refresh force it. DataStore holds settings, speed dial pins, search history and the server list, which supports several servers with one active; switching servers swaps the database. Room also keeps a local play history (timestamp and song id) for History, Forgotten favorites and "Keep listening".
- **Downloads:** Media3 `DownloadManager` and `DownloadService` over a separate `SimpleCache`, using the `download` endpoint, or `stream` at the chosen download quality. Albums and playlists can be downloaded as a whole, with progress shown on their download button and in a Downloads page. The streaming cache is a separate LRU `SimpleCache`, 1 GB by default and adjustable. Offline mode shows only downloaded content and queues stars, scrobbles and play-queue saves for when the server comes back.

## Playback

- Media3 ExoPlayer inside a `MediaLibraryService` with a `MediaLibrarySession`. It provides the media notification (with custom star and shuffle commands), lock screen, Bluetooth and headset controls, audio focus, and pause when headphones are unplugged. Its browsable root (Recently played, Starred, Playlists, Albums) serves Android Auto and other `MediaBrowser` clients.
- Gapless playback between tracks. ReplayGain from the OpenSubsonic `replayGain` fields (`trackGain`, `albumGain`, `trackPeak`, `fallbackGain`) in Off / Track / Album / Auto (album when played in album order) modes with a pre-amp, applied as player volume and clamped to avoid clipping. This stands in for ArchiveTune's EBU R128 normalization.
- Quality settings for Wi-Fi and for mobile data: Original (`format=raw`), or 320 / 256 / 192 / 128 kbps in Opus, MP3 or AAC. Downloads have their own quality setting. The codec line on the player shows what is actually playing.
- Playback speed and pitch (`PlaybackParameters`), skip silence, a sleep timer (minutes or end of song), and the system equalizer (open `ACTION_DISPLAY_AUDIO_EFFECT_CONTROL_PANEL` with the player's audio session).
- The queue is saved locally on every change and restored at launch, together with the position. It is also synced to the server as the Queue screen describes.
- Instant mix / radio: when a song, album or artist radio starts, append `getSimilarSongs2` results and fetch more as the queue nears its end.

## Settings pages

- **Appearance:**
  - Theme (System / Light / Dark), pure black, dynamic theme from artwork, theme color, font.
  - Player background, mini player background, slider style (Standard / Wavy / Thick / Circular / Simple), artwork corner radius (0–36dp, default 16).
  - Grid item size (Big / Small), Quick picks as Cards or List, default tab (Home / Search / Library), disable animations.
- **Player & audio:** streaming quality on Wi-Fi and on mobile, download quality, ReplayGain mode and pre-amp, skip silence, remember queue, haptics, swipe-to-skip sensitivity.
- **Lyrics:** provider order (server first, then LRCLIB), text size and alignment, animation (None / Fade / Glow / Slide / Karaoke / Apple-style), keep the screen on while lyrics show.
- **Storage & downloads:** cache size limit and clear cache, image cache size, the list of downloads with sizes, delete all.
- **Scrobbling:** report plays to Navidrome (on), and a note that Last.fm / ListenBrainz linking happens in Navidrome.
- **Servers** (from the server card):
  - Add, switch, edit and remove servers.
  - Custom headers, music folder filter.
  - Library scan status and a "Scan now" button for admins.
- **Backup & restore:** export and import settings, pins and the server list as JSON through the Storage Access Framework. Passwords are left out and the user re-enters them on import.
- **About:** version, open-source licenses, GPL-3.0 notice, and credit to ArchiveTune for the design.

## Architecture and stack (match ArchiveTune's)

- Kotlin 2.x, AGP 9 with a Gradle version catalog, minSdk 26, compileSdk and targetSdk at the latest stable level (ArchiveTune uses 37). Single activity and edge-to-edge.
- Jetpack Compose with `androidx.compose.material3` 1.5.0-alpha. The Expressive APIs used here are still `@ExperimentalMaterial3ExpressiveApi`: `MaterialExpressiveTheme`, `MotionScheme.expressive()`, `ShortNavigationBar`, `HorizontalCenteredHeroCarousel`, `LoadingIndicator`, `CircularWavyProgressIndicator`, `MaterialShapes`, `ButtonDefaults.shapes()`, `IconButtonDefaults.shapes()`, `titleLargeEmphasized` and the other emphasized styles.
- Navigation Compose, Hilt with hilt-navigation-compose, Room (KSP), DataStore Preferences, Paging 3.
- Media3 1.10+ (exoplayer, session, datasource-okhttp), Coil 3 with the OkHttp fetcher, Ktor 3 with the OkHttp engine, kotlinx.serialization.
- androidx.palette, MaterialKolor, `sh.calvin.reorderable` (queue and playlist reordering), `me.saket.squigglyslider` (wavy slider), `com.valentinilk.shimmer`, Timber.
- MVVM with a unidirectional flow. Composables are stateless and receive a `UiState` from a `@HiltViewModel` that exposes `StateFlow` state and a channel of one-off events. ViewModels call use cases and repositories. Repositories combine the Subsonic API, Room and DataStore, returning cached data first and then fresh data. Keep the API client in its own `:subsonic` Gradle module with no Android UI dependencies, so it is unit-testable on the JVM.
- The player lives in the service. The UI talks to it through a `MediaController` wrapped in a `PlayerConnection` that exposes `StateFlow`s (current item, isPlaying, position, queue, shuffle, repeat).

## Tests and delivery

- Unit tests cover:
  - Token auth (known salt and password give the known md5) and URL normalization (scheme added, trailing `/`, `/app` and `/rest` stripped, base paths kept).
  - Parsing of every endpoint used, from JSON fixtures shaped like the Subsonic / OpenSubsonic spec examples. The fixtures are test resources, never shipped.
  - Error-code mapping, queue operations (move, remove, play next, shuffle keeping the current song first), ReplayGain math, the scrobble threshold, and the palette seed fallback order.
- A GitHub Actions workflow runs `./gradlew lint test assembleDebug` and uploads the APK. Release builds are signed from repository secrets. Never commit a keystore.

## Scope

1. First: Connect, the API layer, Home, Search, Library, Album, Artist, playback with the mini player and the Cinematic player, queue, star and scrobble, with dynamic color from artwork.
2. Then: downloads and offline mode, lyrics, Speed dial, Forgotten favorites, the player and mini player backgrounds, all settings pages, playlist editing, server play-queue sync, multiple servers.
3. Optional, after that: Android Auto polish, crossfade (two ExoPlayer instances with volume ramps), more player designs, a home-screen widget, Cast, tablet two-pane layouts.

Build 1 and 2 completely. Leave clean seams for 3.

## Done means

- It connects to a real Navidrome 0.5x server over https behind a Cloudflare Tunnel (including Cloudflare Access service-token headers) and over plain http on a LAN or Tailscale address.
- Browsing, search, play, seek, skip, star and playlist edits all hit the server. Play counts go up in Navidrome after a listen.
- The app, mini player and player recolor from each song's artwork with animated transitions. Light, dark and pure black all look right.
- A downloaded album plays in airplane mode. The queue and position survive a process kill and a reboot. Notification and Bluetooth controls work.
- `./gradlew lint test assembleDebug` passes with no failing tests.
