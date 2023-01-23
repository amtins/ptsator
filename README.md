# PTSator is an AAC Segments PTS Validator

## How does it work?

In order to detect the decrease in the value of the PTS this tool allows to:

1. provide the URL of the HLS playlist that has direct access to the list of AAC segments
2. provide a comma separated list of AAC segments

Depending on the size of the playlist this tool can take several minutes before the result is displayed.

### Playlist with no errors

If the playlist contains no errors, a JSON object will be displayed containing the `status` at `No errors`, followed by the list of all segments and various related information.

### Playlist with errors

If the playlist contains errors, a JSON object will be displayed containing the `status` at `Error` and `message` containing the index of the problematic segment. This tool will display two segments before the PTS value drops, followed by the problematic segment and finally two segments after the PTS value drops.

## What cases are not handled?

1. HLS playlists containing multiple variants
2. CORS, the HTTP header must be defined as `Access-Control-Allow-Origin: *`

### Non-functioning example

The following example will not work because this tool does not browse playlists containing variants.

```bash
#EXTM3U
#EXT-X-STREAM-INF:BANDWIDTH=150000,RESOLUTION=416x234,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/low/index.m3u8
#EXT-X-STREAM-INF:BANDWIDTH=240000,RESOLUTION=416x234,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/lo_mid/index.m3u8
#EXT-X-STREAM-INF:BANDWIDTH=440000,RESOLUTION=416x234,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/hi_mid/index.m3u8
#EXT-X-STREAM-INF:BANDWIDTH=640000,RESOLUTION=640x360,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/high/index.m3u8
#EXT-X-STREAM-INF:BANDWIDTH=64000,CODECS="mp4a.40.5"
http://example.com/audio/index.m3u8
```