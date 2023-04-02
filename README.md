# m3u Playlist importer for Volumio V2 (and probably V3)

https://github.com/skiphansen/volumio-plugins/tree/master/plugins/miscellanea/m3u_importer

This plugin imports m3u or m3u8 playlists into the Volumio.  
Both simple and extended m3u files are supported.

## Installation

Until this plugin is made available from the Volumio UI it must be installed 
manually using the following procedure.

1. Enable SSH following the instructions found [here](https://volumio.github.io/docs/User_Manual/SSH.html).

2. Connect via ssh using putty or the command line ```ssh volumio@volumio.local```,
the password is volumio.  
If you are unable to connect refer to [Finding Volumio](https://volumio.github.io/docs/Good_to_Knows/Finding_Volumio.html)
for more information.

3. Download and install the plugin by running the following commands:
```
wget https://github.com/skiphansen/volumio-plugins/raw/master/plugins/miscellanea/m3u_importer/m3u_importer.zip
mkdir m3u_importer
cd m3u_importer
miniunzip ../m3u_importer.zip
volumio plugin install
```

## Usage

To import a playlist navigate to Plugins / Installed Plugins on the Volumio 
webpage and then click the "Settings" button for the "Import M3U Playlists" 
plugin.

![](https://github.com/skiphansen/volumio-plugins/blob/public/assets/settings.png)

Fill in the **full path** to the folder containing the playlists you wish to
import.  Note: playlists must have an extension of **.m3u** or **.m3u8**, files
with other extensions are siliently ignored.

Alternately enter the **full path** to a specific playlist.

The path is as seen from the view point of the music library hence it **MUST**
start with INTERNAL, NAS, or USB.  

As a convenience the path is initialized to the root of the first USB drive, 
or NAS server found.

Next select how existing playlists are handled.

| Option | |
|-|-|
| New playlists | Playlists which have been imported previously are silently ignored.  |
| All playlist  | All playlists are imported replacing existing Volumio playlists with the same nam|
| Ask before overwriting | You will be asked if existing an playlist should be replaced or not. |

If you choose the _Ask_ option a dialog will pop up for each playlist which
has been imported previously.

![](https://github.com/skiphansen/volumio-plugins/blob/public/assets/ask.png)

Your options are:
| Response | Action |
|-|-|
| Yes | The M3u playlist is imported replacing existing Volumio playlist.|
| No  | This M3u playlist is skipped.|
| Go  | This M3u playlist and all further playlists are imported replacing existing Volumio playlists.|
| Cancel | No further playlists are imported. |

## File paths

Portable m3u playlists (those that use relative file paths) should import 
without any problems.

The plugin also attempts to import playlists that use absolute paths by making 
some assumptions based on the location of the playlist being imported.  If
these assumptions are incorrect the files referenced by the playlist will not
be found and an error message will be displayed.

![](https://github.com/skiphansen/volumio-plugins/blob/public/assets/error.png)

| Response | Action |
|-|-|
| Continue | Ignore the track and continue processing playlist |
| Ignore Errors | Ignore the track and continue processing playlist, ignore further errors |
| Cancel | Stop importing playlists |

## Compatibility

I have only tested this plugin on a Rpi4, but since it's 100% Javascript and 
has no hardware dependencies I would expect it to run on other platforms 
without a problem.

## Support

Please feel free to create a new [issue](https://github.com/skiphansen/volumio-plugins/issues)
if you run into problems.  The paint is very wet on this plugin and feedback is
welcome.

The plug creates a verbose log file in /tmp/m3u_importer.log, please download 
the log and attach to new issues.

## Volumio V3 note / plugin history

This plugin was originally written in November 2021 just prior to the release of Volumio V3. 
At that time the plugin was successfully tested on the V3 beta.

The plugin was submitted to the Volumio team to on Nov 26, 2021 for inclusion as an "official" plugin.
Unfortunately it was too late for V3.  The PR was rejected
on Feb 12 2022 with a request to resubmit the plugin for V3.

At that point I was very busy with work and didn't have much (any) time for
hobby projects so I didn't investigate further.

This plugin was a result of my whole house sound system project for
my wife and I.  When I finished the "master" node (Volumio instance running
on an Rpi4) for the living rooms (old Yamaha amp and M&K speakers) I
showed to my wife.  While she said nice things about Volumio and the sound
quality she almost immediately went back to listening to Pandora on her iPad 
using the internal speakers.   

What can I say, as is often the case my poor marketing efforts doomed good technology!

Fast forward to April 2023.  A Volumio user ran into issues with the
importer on V3 and asked for help.  We were able to get the importer to work
on V3.435.  None of the problems had anything to do with Volumio V3 (see [#1](https://github.com/skiphansen/volumio-plugins/issues/1) for
the gory details) and no changes were made to the importer.

I had some free time so I thought I'd take a whack at resubmitting the importer
for the V3 store.  After some investigation I decided not to spend the effort
for the following reasons:
1. My Volumio based music player works well, but in reality I've hardly used it over the last two years.
2. The number of people using the importer appears to be fairly low.
3. Volumio now requires an account (paid or free) to access many features and **ANY** plugins.
4. The submission process has changed significantly and it now requires [significant](https://docs.google.com/spreadsheets/d/1eRl7ZlMUjOuWTXcSjBgFmO9RI8a3ZJ1U10pi1CWtWy0/edit#gid=0) testing. While this level of testing is an excellent idea, it's more work that I care to do for a hobby project.

So ... the m3u importer will probably continue to work for V3, but it will never be an official
plugin that can be installed directly from the Volumio store.
