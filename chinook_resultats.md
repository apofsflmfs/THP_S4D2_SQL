# Structure des tables

"albums"
|AlbumId|Title|ArtistId|

"employees"
|EmployeeId|LastName|FirstName|Title|ReportsTo|BirthDate|HireDate|Address|City|State|Country|PostalCode|Phone|Fax|Email

"invoices"
|InvoiceId|CustomerId|InvoiceDate|BillingAddress|BillingCity|BillingState|BillingCountry|BillingPostalCode|Total

"playlists"
|PlaylistId|Name|

"artists"
|ArtistId|Name|

"genres"
|GenreId|Name|

"media_types"
|MediaTypeId|Name|

"tracks"
|TrackId|Name|AlbumId|MediaTypeId|GenreId|Composer|Milliseconds|Bytes|UnitPrice 

"customers"
|CustomerId|FirstName|LastName|Company|Address|City|State|Country|PostalCode|Phone|Fax|Email|SupportRepId

"invoice_items"
|InvoiceLineId|InvoiceId|TrackId|UnitPrice|Quantity  

"playlist_track"
|PlaylistId|TrackId|

# requêtes

* Récupère tous les albums
SELECT * FROM albums;

* Récupère tout les albums dont le titre contient "Great" (indice)
SELECT * FROM albums
WHERE Title LIKE '%Great%';

* Donne moi le nombre total d'albums contenus dans la base (sans regarder les id bien sûr)
SELECT COUNT(AlbumId)
FROM albums;
=> 347

* Supprime tout les albums dont le nom contient "music"
DELETE FROM albums
WHERE Title LIKE '%music%';

=> 343 albums

* Récupère tout les albums écrit par AC/DC
SELECT * FROM artists
WHERE Name LIKE 'AC/DC';
=> ArtistId = 1

SELECT * FROM albums
WHERE ArtistID = 1;
=> 2 résultats

Sinon faire
SELECT * FROM albums
JOIN artists ON artists.ArtistId = albums.ArtistId
WHERE artists.name = 'AC/DC';
=> idem


* Récupère tout les titres des albums de AC/DC
SELECT * FROM albums
JOIN artists ON artists.ArtistId = albums.ArtistId
JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE artists.name = 'AC/DC';

SELECT COUNT(TrackId) FROM albums
JOIN artists ON artists.ArtistId = albums.ArtistId
JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE artists.name = 'AC/DC';
=> 18

* Récupère la liste des titre de l'album "Let There Be Rock"
SELECT * FROM albums
JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE albums.title = 'Let There Be Rock';

* Quel est le prix de cet album ainsi que sa durée totale ?

durée totale:
SELECT SUM(Milliseconds) FROM albums
JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE albums.title = 'Let There Be Rock';
=> 2453259 msec

prix
SELECT SUM(UnitPrice) FROM albums
JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE albums.title = 'Let There Be Rock';
=> 7.92


* Quel est le côut de l'intégralité de la discographie de "Deep Purple" ?
SELECT SUM(UnitPrice) FROM albums
JOIN tracks ON tracks.AlbumId = albums.AlbumId
JOIN artists ON artists.ArtistId = albums.ArtistId
WHERE artists.name = 'Deep Purple';
=> 91.08

* Créé l'album de ton artiste favori en base, en renseignant correctement les trois tables albums, artists et tracks
INSERT INTO artists (name) VALUES ('Alanis Morissette');
=> ArtistId = 276
INSERT INTO albums (Title,ArtistId) VALUES ('Jagged Little Pill','276');
=> AlbumId = 348
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('All I Really Want',348,12,284000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('You Oughta Know',348,12,249000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Perfect',348,12,187000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Hand in My Pocket',348,12,221000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Right Through You',348,12,175000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Forgiven',348,12,300000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('You Learn',348,12,209000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Head over Feet',348,12,267000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Mary Jane',348,12,280000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Ironic',348,12,229000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Not the Doctor',348,12,227000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('Wake Up',348,12,293000,0.79,1);
INSERT INTO tracks (Name, AlbumId, GenreId, Milliseconds,UnitPrice, MediaTypeId) VALUES ('You Oughta Know (Jimmy the Saint Blend)',348,12,250000,0.79,1);
