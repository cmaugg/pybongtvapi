# `pybongtvapi`

`pybongtvapi` is a pythonic interface to the [bong.tv] (http://www.bong.tv) platform.

# Usage

`pybongtvapi` supports direct access to bong.tv's JSON web service:

```python
import pybongtvapi

# log in with your username and password
credentials = pybongtvapi.UserCredentials("john", "doe")
api = pybongtvapi.API(credentials=credentials)

# or, if there is a bong.tv cookie somewhere on your hard disk
api = pybongtvapi.API(cookie='path/to/your/cookie.txt')

```

From here on, all methods outlined in [bong.tv's API specification] (http://help.bong.tv/customer/portal/articles/1292793-freie-api-zur-entwicklung) can be called:

```python

# get list of recordings
recordings = api.list_user_recordings()

# list all channels
channels = api.list_channels()

# let's assume today is 15th of May 2015. now, list today's broadcasts ..
channel_id = 1
api.get_broadcasts(channel_id)
# or tomorrow's broadcast
api.get_broadcasts(channel_id, date='16-05-2015')

# create a recording from a broadcast ID
broadcast_id = 12345
api.create_recording(broadcast_id)

# delete a recording from your BongSpace
recording_id = 56789
api.delete_recording(recording_id)

# search for broadcasts
broadcasts = api.search_broadcasts('heute')
```

You can also work with a higher-level API provided by `pybongtvapi`. You can use the `pybongtvapi.EPG` to access the [BongGuide] (http://www.bong.tv/tv-programm/tabelle/sender/hauptsender/sendungen):

```python
epg = pybongtvapi.EPG(api)

for channel in epg.channels:
  print(channel.name)
  for broadcast in channel.broadcasts:
    print()
    print(broadcast.title)
    print(broadcast.outline)
```

Or use the `pybongtvapi.PVR` to access your personal [BongSpace] (http://www.bong.tv/videorekorder/meine-aufnahmen):

```python
pvr = pybongtvapi.PVR(api)

for recording in pvr.recordings:
  print(recording.title)
  if recording.is_recorded():
    print(recording.url)
```
# Changelog
## 0.2
* bugfix: Recording.is_scheduled() did'nt work

## 0.1
* first public release. successor the [pybongtv] (http://sourceforge.net/projects/pybongtv/) library.

# License

`pybongtvapi` is available under [MIT License](https://github.com/cmaugg/pybongtvapi/raw/master/LICENSE.txt).


# Download

You can download [pybongtvapi.py](https://github.com/cmaugg/pybongtvapi/raw/master/pybongtvapi.py).

Alternatively:

    git clone git@github.com:cmaugg/pybongtvapi