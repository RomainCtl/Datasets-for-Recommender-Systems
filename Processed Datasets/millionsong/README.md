## `train_triplets.txt.zip`

(http://millionsongdataset.com/tasteprofile/)[http://millionsongdataset.com/tasteprofile/]

> "For the donwloadable version, the format is straightforward, we provide (user, song, play count) triplets, and each line looks like this (tab-delimited):"

```
b80344d063b5ccb3212f76538f3d9e43d87dca9e	SOAKIMP12A8C130995	1
b80344d063b5ccb3212f76538f3d9e43d87dca9e	SOAPDEY12A81C210A9	1
...
```

## `mmsongs.csv`

song_id, track_id, title, year, artist_name, release, artist_mbid

## `all_mmsongs.csv`

All fields, see list here: [MillionSongDataset](http://millionsongdataset.com/pages/example-track-description/)

## `lastfm_subset.zip`

[http://millionsongdataset.com/lastfm/](http://millionsongdataset.com/lastfm/)

It is a set of json files. Keys are artist, title, timestamp, similars and tags.

example:
```json
{
    "artist": "string",
    "timestamp": "2011-08-02 20:13:25.674526",
    "similars": [
        ["track_id", "0<int<1"],
    ],
    "tags": [
        ["tag_name", "count"],
    ],
    "track_id": "track_id",
    "title": "string"
}
```
