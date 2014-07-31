beets-spotify
=============

Beets plugin for creating a Spotify playlist from a query

Description
===========
This plugin integrates with beets (http://beets.radbox.org/) and generates playlists from tracks within the Beets library.  Using the Spotify Web API (https://developer.spotify.com/web-api/search-item/), any tracks that can be matched with a Spotify ID are returned, and the results can be either copy/pasted in to a playlist, or opened directly in Spotify.

Why would you want to use this plugin?
* You're a Beets user and Spotify user already
* You have playlists or albums you'd like to make available in Spotify from Beets without having to search for each artist/album/track
* You want to check which tracks in your library are available on Spotify

Installation
============
Save the spotify.py file in this repository to your Beets plugin directory.  For example, on Mac OSX with Python installed using Homebrew (and Beets installed with pip), your plugin should be:

`/Library/Python/2.7/site-packages/beetsplug`

Usage
=====
    Usage: beet spotify [options]

    Options:
      -h, --help            show this help message and exit
      -m MODE, --mode=MODE  "open" to open spotify with playlist, "list" to
                        copy/paste (default)
      -f, --show_failures   Print out list of any tracks that did not match a
                        Sptoify ID
      -v, --verbose         show extra output
      
Example
=======
    Command:
    beet spotify "In The Lonely Hour"

    Output:
    Processing 14 tracks...

    Copy everything between the hashes and paste into a Spotify playlist
    #########################
    http://open.spotify.com/track/19w0OHr8SiZzRhjpnjctJ4
    http://open.spotify.com/track/3PRLM4FzhplXfySa4B7bxS
    http://open.spotify.com/track/0ci6bxPw8muHTmSRs1MOjD
    http://open.spotify.com/track/7IHOIqZUUInxjVkko181PB
    http://open.spotify.com/track/0fySyVgczjbjbxMwNrdwkp
    http://open.spotify.com/track/1VbhR6D6zUoSTBzvnRonXO
    http://open.spotify.com/track/4TBFEe4n95WPxeUYt9jrMe
    http://open.spotify.com/track/2DnBQKrh8aodN4dBSdXAUh
    http://open.spotify.com/track/4DlYkz7xtje3iV2dDBu3OK
    http://open.spotify.com/track/7C6cA8girfd6ZvbkmZmx9V
    http://open.spotify.com/track/6uZ2x1Z6DSpOGAlVlvuhif
    http://open.spotify.com/track/3aoAkxvRjwhXDajp5aSZS6
    http://open.spotify.com/track/7cG68oOj0pZYoSVuP1Jzot
    http://open.spotify.com/track/4qPtIDBT2iVQv13tjpXMDt
    #########################

Configuration Options
=====================
You can add the following options inside config.yaml, descriptions are inline:

    spotify:
        mode: "open" # Default is list, shows the copy/paste output.  open attempts to open directly in Spotify (only tested on Mac)
        region_filter: "US" # Filters tracks by only that market (2-letter code)
        show_faiulres: on # Displays the tracks that did not match a Spotify ID
        tiebreak: "first" # Need to break ties when then are multiple tracks.  Default is popularity.
        regex: [
            {
                field: "albumartist", # Field in the item object to regex
                search: "Something", # String to look for
                replace: "Replaced" # Replacement value
            },
            {
                field: "title",
                search: "Something Else",
                replace: "AlsoReplaced"
            }
        ]