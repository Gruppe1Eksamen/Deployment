<h1>Guide til Gruppe1's Proof of Concept</h1>

***

PoC'et kan tilgås via forbindelsen nedenunder:
http://20.238.91.116:4000/

Hvis man vil køre det lokalt på Mac, skal Branch "Mac" tilgås.

Hvis man vil køre det på Windows, skal Branch "Windows" tilgås.


***
<h3>1. Authentication funktionalitet</h3>

1.1 For at logge ind tilgås dette endpoint, hvor man er authoriseret i 60 minutter.
http://20.238.91.116:4000/api/auth/login

Man kan tilgå eksempelbrugeren, ved at poste denne body:

{
"username": "admin",
"password": "admin"
}

1.2 I authorization tabben, skal der vælges "bearer token" og udstedt token fra login.
Dette skal gøres fremover ved alle API-kald der kræver authentication.
http://20.238.91.116:4000/api/auth/authcheck

***
<h3>2. User funktionalitet</h3>

2.1 Dette POST-kald opretter en user, og kræver ikke authorization.
http://20.238.91.116:4000/api/users/

Body:
{
"username": "admin",
"password": "admin",
"firstName": "admin",
"lastName": "admin",
"address": "123 Main Street",
"phone": "12345678",
"email": "admin@example.com",
"isAdmin": true
}

2.2 Dette GET kald henter en vilkårlig bruger med UserId, og kræver authorization
http://20.238.91.116:4000/api/users/{userid}

2.3 Dette GET kald henter en vilkårlig bruger efter Phone attributten, kræver også authorization.

http://20.238.91.116:4000/api/users/phone/{phone}

2.4 Dette GET kald henter en liste af alle brugere, og kræver ikke authorization af testmæssige formål.

http://20.238.91.116:4000/api/users/

2.5 Dette DELETE kald fjerner en vilkårlig bruger, og kræver authorization.

http://20.238.91.116:4000/api/users/{userid}

2.6 Dette PUT kald opdaterer en vilkårlig User. Der sendes den fulde bruger i Body, og kræver authorization.

http://20.238.91.116:4000/api/users/{userid}

Body:
{
"id": "683599aa454e8ce6fbae1894",
"username": "test",
"password": "test",
"firstName": "admin",
"lastName": "admin",
"address": "123 Main Street",
"phone": "12345678",
"email": "admin@example.com",
"isAdmin": true
}
***
<h3>3. ListingService funktionalitet</h3>

3.1 Dette POST kald opretter et Listing objekt, og kræver authorization.

http://20.238.91.116:4000/api/listing/

Body:
{
"name": "Antique Chair",
"assesedPrice": 250.75,
"description": "A beautiful antique chair in excellent condition.",
"listingCategory": "Furniture",
"location": "Building C",
"sellerId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
"image": [
"http://example.com/images/chair1.jpg",
"http://example.com/images/chair2.jpg"
]
}

3.2 Dette GET kald henter alle Listings og kræver ikke authorization.

http://20.238.91.116:4000/api/listing/

3.3 Dette DELETE kald sletter en vilkårlig Listing, og kræver authorization.

http://20.238.91.116:4000/api/listing/{id}

3.4 Dette PUT kald opdaterer AssessedPrice attributten på en vilkårlig Listing, og kræver authorization. Der indsendes ny pris i Body.

http://20.238.91.116:4000/api/listing/{id}/price
Body:
420

3.5 Dette GET kald henter en vilkårlig Listing efter Id, og kræver authorization.

http://20.238.91.116:4000/api/listing/{id}


***

<h3>4. AuctionService Funktionalitet</h3>

4.1 Dette POST kald opretter Auction objekter ud fra Listing objekter. Det kræver  authorization.
Listings der allerede eksisterer på Auctions, bliver ikke oprettet.

http://20.238.91.116:4000/api/auction/generate

4.2 Dette GET kald henter alle auctions, og kræver authorization.

http://20.238.91.116:4000/api/auction/

4.3 Dette POST kald ændrer AuctionStatus på en vilkårlig Auction til Open. Den kræver authorization.

http://20.238.91.116:4000/api/auction/{auctionId}/open

4.4 Dette POST kald indsætter et bud på en vilkårlig auktion, og kræver auhtorization. I body insendes UserId og BidAmount. 
Der kan kun bydes på Auctions med AuctionStatus sat til Open.

http://20.238.91.116:4000/api/auction/{auctionId}/bid

Body:
{
"UserId": "68359689454e8ce6fbae1893",
"BidAmount": "1234"
}

4.5 Dette POST kald ændrer AuctionStatus på en vilkårlig Auction til CLosed. Her udvælges der en Winner og WinningBid. Den kræver Authorization.

http://20.238.91.116:4000/api/auction/{auctionId}/closed

4.6 Dette GET kald ser vinderen af en vilkårlig Auction, og kræver authorization.

http://20.238.91.116:4000/api/auction/{auctionId}/winner

4.7 Dette GET kald ser alle Auctions en vilkårlig bruger har vundet (WinnerUserId). Det kræver authorization.

http://20.238.91.116:4000/api/auction/winner/{winnerId}

4.8 Dette PUT kald ændrer værdien for PickUp attributten på Auction objektet, og kræver authorization.

http://20.238.91.116:4000/api/auction/{auctionId}/pickup