# Musicbrainz

[https://musicbrainz.org/][https://musicbrainz.org/]

* `tracks.csv`: \
id, gid, name, artist_name, album_name, language, date_year, date_month, date_day, rating, rating_count, url, covert_art_url, artist_mbid

* `genres`: \
id, gid, name

* `tags`: \
id, name

* `track_tags`: \
recording, tag, count


## SQL query

Track (recording) (count: 23 177 641):
```SQL
SELECT rec.id, rec.gid, rec.name, acn.name AS artist_name, re.name AS album_name,
la.iso_code_1 AS language, ruc.date_year, ruc.date_month, ruc.date_day,
meta.rating, meta.rating_count, url.url,
CASE WHEN ca.id IS NOT NULL
	THEN CONCAT('http://coverartarchive.org/release/', rec.gid, '/', ca.id, '.', imgt.suffix)
	ELSE NULL
END AS cover_art_url, ar.gid AS artist_mbid
FROM musicbrainz.recording as rec
LEFT OUTER JOIN musicbrainz.artist_credit AS ac ON ac.id=rec.artist_credit
LEFT OUTER JOIN musicbrainz.artist_credit_name AS acn ON ac.id=acn.artist_credit AND acn.position=0
LEFT OUTER JOIN musicbrainz.artist AS ar ON ar.id=acn.artist
LEFT OUTER JOIN (SELECT DISTINCT ON (entity0) entity0, entity1 FROM musicbrainz.l_recording_release) AS lrr ON lrr.entity0=rec.id
LEFT OUTER JOIN musicbrainz.release AS re ON re.id=lrr.entity1
LEFT OUTER JOIN musicbrainz.language AS la ON la.id=re.language
LEFT OUTER JOIN musicbrainz.release_unknown_country AS ruc ON ruc.release=re.id
LEFT OUTER JOIN musicbrainz.recording_meta AS meta ON meta.id=rec.id
LEFT OUTER JOIN (SELECT DISTINCT ON (entity0) entity0, entity1 FROM musicbrainz.l_recording_url) AS lru ON lru.entity0=rec.id
LEFT OUTER JOIN musicbrainz.url AS url ON lru.entity1=url.id
LEFT OUTER JOIN cover_art_archive.cover_art AS ca ON rec.id=ca.release AND ca.ordering=1
LEFT OUTER JOIN cover_art_archive.image_type AS imgt ON ca.mime_type=imgt.mime_type
ORDER BY rec.id ASC;
```

Tracks tags (count: 1 552 878):
```SQL
SELECT recording, tag, count FROM musicbrainz.recording_tag ORDER BY recording ASC, tag ASC;
```

Tags (count: 101 085):
```SQL
SELECT id, name FROM musicbrainz.tag;
```

Genres (count: 485):
```SQL
SELECT id, gid, name FROM musicbrainz.genre ORDER BY id ASC;
```
