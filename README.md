

---
# Bazy danych


**Autorzy:** Mikołaj Durkot, Jakub Pomorski, Dawid Wójtowicz

---

- [1. Wymagania i funkcje systemu](#1-wymagania-i-funkcje-systemu)
- [2. Baza danych](#2-baza-danych)
    - [Schemat bazy danych](#schemat-bazy-danych)
    - [Opis poszczególnych tabel](#opis-poszczególnych-tabel)
      - [Attractions](#attractions)
      - [Companies](#companies)
      - [Countries](#countries)
      - [Customers](#customers)
      - [GuestDetails](#guestdetails)
      - [Guests](#guests)
      - [Trips](#trips)
      - [ReservationDetails](#reservationdetails)
      - [Reservations](#reservations)
- [3. Widoki](#3-widoki)
    - [1. Widok wypisujący rezerwacje, ceny wycieczek, kwotę do zapłaty, zapłacone i do zapłaty](#1-widok-wypisujący-rezerwacje-ceny-wycieczek-kwotę-do-zapłaty-zapłacone-i-do-zapłaty)
    - [2. Widok zapełnionych miejsc w atrakcji w stosunku do miejsc wykupionych](#2-widok-zapełnionych-miejsc-w-atrakcji-w-stosunku-do-miejsc-wykupionych)
    - [3. Widok pozostałych wolnych miejsc dla atrakcji](#3-widok-pozostałych-wolnych-miejsc-dla-atrakcji)
    - [4. Widok zawierający wykaz gości](#4-widok-zawierający-wykaz-gości)
    - [5. Widok wypisujący gości atrakcji.](#5-widok-wypisujący-gości-atrakcji)
    - [6. Widok wypisujący najważniejsze informacje o wycieczkach.](#6-widok-wypisujący-najważniejsze-informacje-o-wycieczkach)
- [4. Funkcje](#4-funkcje)
    - [1. Funkcja obliczająca kwotę do zapłaty za całą rezerwację wraz z atrakcjami.](#1-funkcja-obliczająca-kwotę-do-zapłaty-za-całą-rezerwację-wraz-z-atrakcjami)
    - [2. Funkcja wypisująca liczbę pozostałych miejsc na wycieczkę.](#2-funkcja-wypisująca-liczbę-pozostałych-miejsc-na-wycieczkę)
    - [3. Funkcja wypisująca liczbę pozostałych miejsc na atrakcję.](#3-funkcja-wypisująca-liczbę-pozostałych-miejsc-na-atrakcję)
    - [4. Funkcja wypisująca gościa i atrakcje na które się wybiera.](#4-funkcja-wypisująca-gościa-i-atrakcje-na-które-się-wybiera)
    - [5. Funkcja zwracająca kwotę do zapłaty za wycieczkę wraz z atrakcjami dla gościa](#5-funkcja-zwracająca-kwotę-do-zapłaty-za-wycieczkę-wraz-z-atrakcjami-dla-gościa)
    - [6. Funkcja zwracająca kwotę do zapłaty za wycieczkę wraz z atrakcjami za całość](#6-funkcja-zwracająca-kwotę-do-zapłaty-za-wycieczkę-wraz-z-atrakcjami-za-całość)
- [5. Procedury](#5-procedury)
    - [1. Procedura dodająca klienta lub firmę](#1-procedura-dodająca-klienta-lub-firmę)
    - [2. Procedura dodająca rezerwację (bez atrakcji - te później).](#2-procedura-dodająca-rezerwację-bez-atrakcji---te-później)
    - [3. Procedura dodająca atrakcje do rezerwacji](#3-procedura-dodająca-atrakcje-do-rezerwacji)
    - [4. Procedura wyświetlająca płatności w podanym okresie czasu](#4-procedura-wyświetlająca-płatności-w-podanym-okresie-czasu)
    - [5. Procedura dodająca gościa do atrakcji](#5-procedura-dodająca-gościa-do-atrakcji)
    - [6. Procedura dodająca gościa do rezerwacji](#6-procedura-dodająca-gościa-do-rezerwacji)
    - [7. Procedura zmieniająca rezerwację](#7-procedura-zmieniająca-rezerwację)
    - [8. Procedura usuwająca gościa](#8-procedura-usuwająca-gościa)
    - [9. Procedura usuwająca gościa z atrakcji](#9-procedura-usuwająca-gościa-z-atrakcji)
    - [10. Procedura usuwająca rezerwację](#10-procedura-usuwająca-rezerwację)
- [Do zrobienia](#do-zrobienia)
---

# 1.	Wymagania i funkcje systemu

Wymagania:
- Informacje o cenie i zawartości wycieczek
- Przewoźnicy
- Opiekunowie i przewodnicy
- Tabela klientów i turystów
- Miasta i ich atrakcje
- Kontrola dat wycieczek np. 7 dni przed jej startem

Funkcje admina:
- Wyświetlanie bazy użytkowników i wycieczek
- Tworzenie nowych wycieczek
- Usuwanie nieaktualnych wycieczek
- Modyfikacja aktualnych wycieczek (ceny i dostępne podopcje)

Funkcje klienta:
- Wyświetlanie dostępnych wycieczek
- Wyświetlanie dodatkowych opcji dla każdej wycieczki
- Zapisywanie turystów (niekoniecznie klienta) na wycieczki
- Wypisanie na min. 7 dni przed startem wycieczki.
- Prośba o realizację prywatnej wycieczki (info o niej mają admin i klient oraz jej uczestnicy).

# 2.    Baza danych

### Schemat bazy danych
![DIAGRAM](diagram.png)
### Opis poszczególnych tabel:
- #### Attractions
Tabela ta opisuje poszczególne atrakcje dla każdej wycieczki.

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| AttractionID | int | ID Atrakcji do identyfikacji |
| TripID | int | ID Wycieczki |
| Name |  varchar(50) | Nazwa atrakcji |
| Address | varchar(50) | Adres atrakcji (miejsce/region) |
| Spots | int | Maks. liczba uczestnikow |
| Price | decimal(19, 2) | Cena za pojedynczą atrakcję |

```sql
-- Tabela: Attractions
CREATE TABLE Attractions (
    AttractionID int IDENTITY(1,1) NOT NULL,
    TripID int  NOT NULL,
    Name varchar(50)  NOT NULL,
    Address varchar(50)  NOT NULL,
    Spots int  NOT NULL,
    Price decimal(19, 2)  NOT NULL,
    CONSTRAINT Attractions_pk PRIMARY KEY  (AttractionID)
);

--Powiązanie: Attractions_Trips
ALTER TABLE Attractions ADD CONSTRAINT Attractions_Trips
    FOREIGN KEY (TripID)
    REFERENCES Trips (TripID);
```


- #### Companies
Tabela ta zawiera dane o firmach, które kupują u nas wycieczki.
| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| CustomerID   | int    |  ID klienta do identyfikacji          |
| CompanyName | varchar(50) | Nazwa firmy |
| Address | varchar(50) | Adres firmy |
| ContactNumber | varchar(15) | Numer telefonu do kontaktu |

```sql
-- Tabela: Companies
CREATE TABLE Companies (
    CustomerID int  NOT NULL,
    CompanyName varchar(50)  NOT NULL,
    Address varchar(50)  NOT NULL,
    ContactNumber varchar(15)  NOT NULL,
    CONSTRAINT Companies_pk PRIMARY KEY  (CustomerID)
);

-- Powiązanie: Companies_Customers 
ALTER TABLE Companies ADD CONSTRAINT Companies_Customers
    FOREIGN KEY (CustomerID)
    REFERENCES Customers (CustomerID);
```

- #### Countries
Tabela słownikowa zawierająca nazwę kraju dla każdego 3-literowego kodu państwa zgodnie ze standardem ISO 3166-1 alfa-3.
| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| CountryID | varchar(3) | ID Państwa |
| CountryName | varchar(50) | Nazwa państwa |

```sql
-- Tabela: Countries
CREATE TABLE Countries (
    CountryID varchar(3)  NOT NULL,
    CountryName varchar(50)  NOT NULL,
    CONSTRAINT Countries_pk PRIMARY KEY  (CountryID)
);
```
- #### Customers
Tabela ta zawiera podstawowe informacje o kliencie - jego id i kraj.
| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| CustomerID | int | ID Klienta |
| CountryID | varchar(3) | ID Państwa |

```sql
-- Tabela: Customers
CREATE TABLE Customers (
    CustomerID int IDENTITY(1,1) NOT NULL,
    CountryID varchar(3)  NOT NULL,
    CONSTRAINT CustomerID PRIMARY KEY  (CustomerID)
);

-- Powiązanie: Customers_Countries 
ALTER TABLE Customers ADD CONSTRAINT Customers_Countries
    FOREIGN KEY (CountryID)
    REFERENCES Countries (CountryID);
```
- #### GuestDetails
Tabela ta zawiera pary gość-atrakcja, służące do powiązania poszczególnych gości do poszczególnych atrakcji.
| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| GuestID | int | ID Gościa |
| ReservationID | int | ID Rezerwacji |
| AttractionID | int | ID Atrakcji |

```sql
-- Tabela: GuestDetails
CREATE TABLE GuestDetails (
    GuestID int  NOT NULL,
    ReservationID int  NOT NULL,
    AttractionID int  NOT NULL,
    CONSTRAINT GuestDetails_pk PRIMARY KEY  (GuestID,ReservationID,AttractionID)
);

-- Powiązanie: GuestsDetails_Guests 
ALTER TABLE GuestDetails ADD CONSTRAINT GuestsDetails_Guests
    FOREIGN KEY (GuestID)
    REFERENCES Guests (GuestID);

-- Powiązanie: GuestDetails_ReservationDetails
ALTER TABLE GuestDetails ADD CONSTRAINT GuestDetails_ReservationDetails
    FOREIGN KEY (ReservationID,AttractionID)
    REFERENCES ReservationDetails (ReservationID,AttractionID)
```

- #### Guests
Tabela zawiera informacje o uczestnikach wycieczki.
| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| GuestID | int | ID Gościa |
| ReservationID | int | ID Rezerwacji |
| FirstName | varchar(50) | Imię gościa |
| LastName | varchar(50) | Nazwisko gościa |

```sql
-- Tabela: Guests
CREATE TABLE Guests (
    GuestID int IDENTITY(1,1) NOT NULL,
    ReservationID int  NOT NULL,
    FirstName varchar(50)  NOT NULL,
    LastName varchar(50)  NOT NULL,
    CONSTRAINT Guests_pk PRIMARY KEY  (GuestID)
);

-- Powiązanie: Reservations_Guests
ALTER TABLE Guests ADD CONSTRAINT Reservations_Guests
    FOREIGN KEY (ReservationID)
    REFERENCES Reservations (ReservationID);
```

- #### Trips
Tabela opisująca wycieczki znajdujące się w stałej ofercie.

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| TripID | int | ID Wycieczki |
| CountryID | varchar(3) | ID Kraju |
| Spots | int | Maksymalna ilość miejsc na wycieczce |
| StartDate | date | Data rozpoczęcia wycieczki |
| EndDate | date | Data zakończenia wycieczki |
| Price | int | Cena całej wycieczki (nie wliczając atrakcji) |
| AvailableFrom | date | Data od której wycieczka jest dostępna do zakupu |

```sql
-- Tabela: Trips
CREATE TABLE Trips (
    TripID int IDENTITY(1,1) NOT NULL,
    CountryID varchar(3)  NOT NULL,
    Spots int  NOT NULL,
    StartDate date  NOT NULL,
    EndDate date  NOT NULL,
    Price decimal(19, 2)  NOT NULL,
    AvailableFrom date  NOT NULL,
    CONSTRAINT TripID PRIMARY KEY  (TripID)
);

-- Powiązanie: Trips_Countries
ALTER TABLE Trips ADD CONSTRAINT Trips_Countries
    FOREIGN KEY (CountryID)
    REFERENCES Countries (CountryID);
```

- #### ReservationDetails
Tabela zawiera informacje wiążace rezerwacje z wykupionymi atrakcjami.

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| AttractionID | int | ID Atrakcji |
| ReservationID  | int | ID Rezerwacji |
| AttendeesNumber | int | Ilość gości przypisanych do danej atrakcji |
| Price  | decimal(19,2) | Cena atrakcji za jedną osobę w momencie zakupu |

```sql
-- Tabela: ReservationDetails
CREATE TABLE ReservationDetails (
    AttractionID int  NOT NULL,
    ReservationID int  NOT NULL,
    AttendeesNumber int  NOT NULL,
    Price decimal(19,2) NOT NULL,
    CONSTRAINT ReservationDetails_pk PRIMARY KEY  (ReservationID,AttractionID)
);

-- Powiązanie: ReservationDetails_Attractions 
ALTER TABLE ReservationDetails ADD CONSTRAINT ReservationDetails_Attractions
    FOREIGN KEY (AttractionID)
    REFERENCES Attractions (AttractionID);

-- Powiązanie: ReservationDetails_Reservations 
ALTER TABLE ReservationDetails ADD CONSTRAINT ReservationDetails_Reservations
    FOREIGN KEY (ReservationID)
    REFERENCES Reservations (ReservationID);
```

- #### Reservations
Tabela zawiera informacje dotyczące poszczególnych rezerwacji.

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| ReservationID | int | ID Rezerwacji |
| CustomerID  | int | ID Klienta |
| TripID | int  | ID Wycieczki |
| Spots | int | Ilość zarezerwowanych miejsc |
| ReservationDate | date | Data zakupu rezerwacji |
| Price | decimal(19,2) | Cena rezerwacji pobierana w momencie zakupu |
| IsActive | bit | Status rezerwacji (aktywna/anulowana) |

```sql
-- Tabela: Reservations
CREATE TABLE Reservations (
    ReservationID int  NOT NULL,
    CustomerID int  NOT NULL,
    TripID int  NOT NULL,
    Spots int  NOT NULL,
    ReservationDate date  NOT NULL,
    Price decimal(19,2)  NOT NULL,
    IsActive bit NOT NULL,
    CONSTRAINT Reservations_pk PRIMARY KEY  (ReservationID)
);

-- Wartości domyślne:
    ALTER TABLE Reservations ADD  CONSTRAINT DEFAULT_Reservations_ReservationDate  DEFAULT (getdate()) FOR ReservationDate
    
    ALTER TABLE Reservations ADD  CONSTRAINT DEFAULT_Reservations_IsActive  DEFAULT ((1)) FOR IsActive


-- Powiązanie: Reservations_Customers 
ALTER TABLE Reservations ADD CONSTRAINT Reservations_Customers
    FOREIGN KEY (CustomerID)
    REFERENCES Customers (CustomerID);


-- Powiązanie: Reservations_Trips 
ALTER TABLE Reservations ADD CONSTRAINT Reservations_Trips
    FOREIGN KEY (TripID)
    REFERENCES Trips (TripID);
```



- #### PrivateClients
Tabela zawiera informacje o klientach, którzy są osobami prywatnymi.

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| CustomerID  |   int  |   ID Klienta    |
| FirstName    |  varchar(50)  |  Imię klienta       |
| LastName    |  varchar(50)  |   Nazwisko klienta       |
| Address    |  varchar(50)  |   Adres klienta     |
| ContactNumber | varchar(15) | Numer telefonu klienta (razem z numerem kierunkowym) |

```sql
-- Tabela: PrivateClients
CREATE TABLE PrivateClients (
    CustomerID int  NOT NULL,
    FirstName varchar(50)  NOT NULL,
    LastName varchar(50)  NOT NULL,
    Address varchar(50)  NOT NULL,
    ContactNumber varchar(15)  NOT NULL,
    CONSTRAINT PrivateClients_pk PRIMARY KEY  (CustomerID)
);

-- Powiązanie: PrivateClients_Customers 
ALTER TABLE PrivateClients ADD CONSTRAINT PrivateClients_Customers
    FOREIGN KEY (CustomerID)
    REFERENCES Customers (CustomerID);
```


- #### Payments
Tabela zawiera informacje dotyczące płatności. 

| Nazwa atrybutu | Typ | Opis/Uwagi |
| -------------- | --- | ---------- |
| PaymentID | int  | ID Płatności |
| ReservationID | int | ID Rezerwacji |
| Amount | decimal(19,2) | Wartość płatności |
| PaymentDate | date | Data zaksięgowania płatności |
| PaymentMethod | varchar(50) | Metoda płatności |

```sql
-- Tabela: Payments
CREATE TABLE Payments (
    PaymentID int  NOT NULL,
    ReservationID int  NOT NULL,
    Amount decimal(19,2)  NOT NULL,
    PaymentDate date  NOT NULL,
    PaymentMethod varchar(50)  NOT NULL,
    CONSTRAINT Payments_pk PRIMARY KEY  (PaymentID)
);

-- Wartości domyślne:
    ALTER TABLE Payments ADD  CONSTRAINT DEFAULT_Payments_PaymentDate  DEFAULT (getdate()) FOR PaymentDate

-- Powiązanie: Payments_Reservations
ALTER TABLE Payments ADD CONSTRAINT Payments_Reservations
    FOREIGN KEY (ReservationID)
    REFERENCES Reservations (ReservationID);
```
# 3. Widoki

## 1. Widok wypisujący rezerwacje, ceny wycieczek, kwotę do zapłaty, zapłacone i do zapłaty
```sql
create or ALTER view PaymentsInfo as
(
select IsActive,ReservationID,TripID,CustomerID, dbo.res_full_cost(ReservationID) as Price,
dbo.res_all_payments(ReservationID) as Paid, 
dbo.res_full_cost(ReservationID) - dbo.res_all_payments(ReservationID) as LeftToPay
from Reservations r
)
```

## Przykład użycia
![vprzyklad1](przyklady/views/PaymentsInfo.png)

## 2. Widok zapełnionych miejsc w atrakcji w stosunku do miejsc wykupionych
```sql
CREATE OR ALTER view SpotCheck as
select t.TripID,a.AttractionID, count(gd.GuestID) as PlacesTaken,
isnull(rd.AttendeesNumber,0) as PlacesReserved from Attractions a
left join ReservationDetails rd on rd.AttractionID=a.AttractionID
and rd.ReservationID not in (select ReservationID from Reservations where IsActive=0)
left join GuestDetails gd on rd.ReservationID=gd.ReservationID and rd.AttractionID=gd.AttractionID
join Trips t on t.TripID=a.TripID
group by a.AttractionID, rd.AttendeesNumber,t.TripID

```

## Przykład użycia
![vprzyklad2](przyklady/views/spotcheck.png)

## 3. Widok pozostałych wolnych miejsc dla atrakcji
```sql
CREATE OR ALTER VIEW atstatus AS
SELECT t.TripID, a.AttractionID, a.Name as AttractionName, 
       ISNULL(a.Spots - SUM(ISNULL(rd.AttendeesNumber, 0)), a.Spots) as FreeSpots
FROM Trips t
LEFT JOIN Attractions a on t.TripID = a.TripID
LEFT JOIN Reservations r on t.TripID = r.TripID and r.ReservationID not in (select ReservationID from Reservations where IsActive=0)
LEFT JOIN ReservationDetails rd on r.ReservationID = rd.ReservationID AND a.AttractionID = rd.AttractionID
GROUP BY t.TripID, a.AttractionID, a.Spots, a.Name;
```
## Przykład użycia
![vprzyklad3](przyklady/views/atstatus.png)

## 4. Widok zawierający wykaz gości
```sql
CREATE or ALTER VIEW GuestList AS
SELECT g.GuestID, g.FirstName, g.LastName, t.TripID, g.ReservationID, t.CountryID,
t.StartDate, t.EndDate, COALESCE(CAST(a.AttractionID as varchar), 'None') as AttractionID,
ISNULL(a.Name, 'None') as AttractionName FROM Guests g JOIN
Reservations r ON g.ReservationID = r.ReservationID and r.ReservationID not in (select ReservationID from Reservations where IsActive=0)
JOIN Trips t ON r.TripID = t.TripID LEFT JOIN GuestDetails gd ON g.GuestID = gd.GuestID AND g.ReservationID = gd.ReservationID
LEFT JOIN Attractions a ON gd.AttractionID = a.AttractionID AND t.TripID = a.TripID;
```
## Przykład użycia
![vprzyklad4](przyklady/views/guestlist.png)

## 5. Widok wypisujący gości atrakcji.
```sql
create or ALTER view AttrInfo as
(
select g.ReservationID,a.AttractionID,a.Name,g.FirstName,g.LastName from GuestDetails gd
join Guests g on gd.GuestID=g.GuestID
join Attractions a on gd.AttractionID=a.AttractionID
where gd.ReservationID not in (select ReservationID from Reservations where IsActive=0)
)
```
## Przykład użycia
![vprzyklad5](przyklady/views/AttrInfo.png)

## 6. Widok wypisujący najważniejsze informacje o wycieczkach.
```sql
create or ALTER VIEW FullTripInfo AS
(
select t.TripID,t.Price,dbo.trip_avail(t.TripID) as FreeTripSpots,
a.AttractionID,a.Name,a.Price as AtPrice,dbo.attr_avail(a.AttractionID) as FreeAttractionSpots,
t.CountryID, t.StartDate, t.EndDate, t.AvailableFrom
from Trips t join Attractions a on t.TripID=a.TripID
)
```
## Przykład użycia
![vprzyklad6](przyklady/views/FullTripInfo.png)

# 4. Funkcje

## 1. Funkcja obliczająca kwotę do zapłaty za całą rezerwację wraz z atrakcjami.
```sql
CREATE or ALTER FUNCTION [dbo].[res_full_cost](@ReservationID INT)
RETURNS DECIMAL(19, 2)
AS
BEGIN
    DECLARE @CalkowityKoszt DECIMAL(19, 2);

    SELECT @CalkowityKoszt = isnull((
        SELECT r.Price*r.Spots
        FROM Reservations r
        WHERE r.ReservationID = @ReservationID
        
    ),0) + isnull((
        SELECT SUM(rd.Price * rd.AttendeesNumber) 
        FROM ReservationDetails rd
        WHERE rd.ReservationID = @ReservationID
    ),0);

    RETURN @CalkowityKoszt;
END;
```
## Przykład użycia
![fprzyklad1](przyklady/functions/resfullcost.png)

## 2. Funkcja wypisująca liczbę pozostałych miejsc na wycieczkę.
```sql
CREATE or ALTER FUNCTION [dbo].[trip_avail](@tripID INT)
RETURNS INT
AS
BEGIN
    DECLARE @totalSpots INT;
    DECLARE @reservedSpots INT;
    
    SELECT @totalSpots = Spots FROM Trips WHERE TripID = @tripID;
    
    SELECT @reservedSpots = isnull(sum(Spots),0) FROM Reservations WHERE TripID = @tripID
    and ReservationID not in (select ReservationID from Reservations where IsActive=0)
    
    RETURN @totalSpots - @reservedSpots;
END;
```
## Przykład użycia
![fprzyklad2](przyklady/functions/tripavail.png)

## 3. Funkcja wypisująca liczbę pozostałych miejsc na atrakcję.
```sql
CREATE or ALTER FUNCTION [dbo].[attr_avail](@attractionID INT)
RETURNS INT
AS
BEGIN
    DECLARE @totalSpots INT;
    DECLARE @reservedSpots INT;
    
    SELECT @totalSpots = Spots FROM Attractions WHERE AttractionID = @attractionID;
    
    SELECT @reservedSpots = isnull(SUM(AttendeesNumber),0) FROM ReservationDetails WHERE AttractionID = @attractionID 
    and ReservationID not in (select ReservationID from Reservations where IsActive=0);
    
    RETURN @totalSpots - @reservedSpots;
END;
```
## Przykład użycia
![fprzyklad3](przyklady/functions/attravail.png)

## 4. Funkcja wypisująca gościa i atrakcje na które się wybiera.
```sql
create or ALTER FUNCTION [dbo].[guest_attr]
(
    @GuestID INT
)
RETURNS TABLE
AS
RETURN
(
    select gd.ReservationID,gd.AttractionID,rd.Price 
    from GuestDetails gd
    join ReservationDetails rd on 
    rd.ReservationID=gd.ReservationID
    and rd.AttractionID=gd.AttractionID
    where gd.GuestID=@GuestID
);
```
## Przykład użycia
![fprzyklad4](przyklady/functions/guestattr.png)

## 5. Funkcja zwracająca kwotę do zapłaty za wycieczkę wraz z atrakcjami dla gościa
```sql
create or ALTER FUNCTION [dbo].[guest_full_cost](@GuestID INT, @ReservationID INT)
RETURNS DECIMAL(19, 2)
AS
BEGIN
    DECLARE @CalkowityKoszt DECIMAL(19, 2);

    SELECT @CalkowityKoszt = isnull((
        SELECT r.Price
        FROM Reservations r
        join Guests g on r.ReservationID=g.ReservationID 
        WHERE g.GuestID = @GuestID and r.ReservationID=@ReservationID
        
    ),0) + isnull((
        select sum(price) from dbo.guest_attr(@GuestID) 
        where ReservationID = @ReservationID
    ),0);

    RETURN @CalkowityKoszt;
END;
```
## Przykład użycia
![fprzyklad5](przyklady/functions/guestfullcost.png)

## 6. Funkcja zwracająca kwotę do zapłaty za wycieczkę wraz z atrakcjami za całość
```sql
create or ALTER FUNCTION [dbo].[res_all_payments](@ReservationID INT)
RETURNS DECIMAL(19, 2)
AS
BEGIN
    DECLARE @CalkowityKoszt DECIMAL(19, 2);

    SELECT @CalkowityKoszt = isnull((
        select sum(Amount) from Payments p
        where ReservationID=@ReservationID
    ),0);

    RETURN @CalkowityKoszt;
END;
```
## Przykład użycia
![fprzyklad6](przyklady/functions/resallpayments.png)

# 5. Procedury

## 1. Procedura dodająca klienta lub firmę
```sql
CREATE OR ALTER PROC p_add_customer
@customerType CHAR(1),  -- 'P' for Private Client, 'C' for Company
@countryid VARCHAR(3), 
@firstname VARCHAR(50) = NULL, 
@lastname VARCHAR(50) = NULL, 
@companyname VARCHAR(50) = NULL, 
@address VARCHAR(50), 
@contactnumber VARCHAR(15)
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Check if the CountryID exists
        IF NOT EXISTS (SELECT * FROM Countries WHERE CountryID = @countryid)
            THROW 50003, 'No country with this CountryID', 1;

        -- Check if ContactNumber starts with '+'
        IF LEFT(@contactnumber, 1) <> '+'
            THROW 50003, 'ContactNumber should start with +', 1;

        -- Insert into Customers table
        INSERT INTO Customers (CountryID) VALUES (@countryid);

        DECLARE @CustomerID INT
        SET @CustomerID = SCOPE_IDENTITY();

        -- Insert into either Companies or PrivateClients based on @customerType
        IF @customerType = 'C'
        BEGIN
            -- Check if CompanyName is provided
            IF @companyname IS NULL
                THROW 50003, 'CompanyName is required for companies', 1;

            INSERT INTO Companies (CustomerID,CompanyName, Address, ContactNumber) 
            VALUES (@CustomerID,@companyname, @address, @contactnumber);
        END
        ELSE IF @customerType = 'P'
        BEGIN
            -- Check if FirstName and LastName are provided
            IF @firstname IS NULL OR @lastname IS NULL
                THROW 50003, 'FirstName and LastName are required for private clients', 1;

            INSERT INTO PrivateClients (CustomerID,FirstName, LastName, Address, ContactNumber) 
            VALUES (@CustomerID,@firstname, @lastname, @address, @contactnumber);
        END
        ELSE
        BEGIN
            THROW 50003, 'Invalid customer type. Use ''P'' for Private Client or ''C'' for Company', 1;
        END

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad1](przyklady/procedures/addcustomer.png)

## 2. Procedura dodająca rezerwację (bez atrakcji).
```sql
CREATE OR ALTER PROCEDURE p_add_reservation
    @CustomerID INT,
    @TripID INT,
    @Spots INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie czy TripID istnieje
        IF NOT EXISTS (SELECT * FROM Trips WHERE TripID = @TripID)
            THROW 50001, 'No trip with this TripID.', 1;

        -- Pobranie liczby miejsc w wycieczce
        DECLARE @TripSpots INT;
        SELECT @TripSpots = Spots FROM Trips WHERE TripID = @TripID;

        -- Obliczenie liczby zarezerwowanych miejsc
        DECLARE @ReservedSpots INT;
        SELECT @ReservedSpots = ISNULL(SUM(Spots), 0) FROM Reservations WHERE TripID = @TripID;

        -- Sprawdzenie dostępnych miejsc
        IF @Spots > (@TripSpots - @ReservedSpots)
            THROW 50002, 'Not enough available spots for this trip.', 1;

        declare @today date;
        select @today = getdate()

        IF @today < (SELECT AvailableFrom FROM Trips WHERE TripID = @TripID)
            THROW 50003, 'You cannot make a reservation for this trip yet. :(', 1;

        IF DATEDIFF(DAY, @today, (SELECT StartDate FROM Trips WHERE TripID = @TripID)) < 7
            THROW 50004, 'Time to make reservations for this trip is over. :(', 1;

        -- Pobranie ceny wycieczki
        DECLARE @TripPrice DECIMAL(19, 2);
        SELECT @TripPrice = Price FROM Trips WHERE TripID = @TripID;

        -- Dodanie nowej rezerwacji
        INSERT INTO Reservations (CustomerID, TripID, Spots, ReservationDate, Price)
        VALUES (@CustomerID, @TripID, @Spots, @today, @TripPrice);

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad2](przyklady/procedures/addreservation.png)

## 3. Procedura dodająca atrakcje do rezerwacji 
```sql
CREATE OR ALTER PROCEDURE p_add_attr_reservation
    @ReservationID INT,
    @AttractionID INT,
    @AttendeesNumber INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie, czy istnieje rezerwacja o podanym ID
        IF @AttendeesNumber < 1
            THROW 50001, 'You cannot make a reservation with zero or less people.', 1;

        -- Sprawdzenie, czy istnieje rezerwacja o podanym ID
        IF NOT EXISTS (SELECT * FROM Reservations WHERE ReservationID = @ReservationID)
            THROW 50002, 'No reservation with this ReservationID.', 1;

        -- Sprawdzenie, czy istnieje atrakcja o podanym ID
        IF NOT EXISTS (SELECT * FROM Attractions WHERE AttractionID = @AttractionID)
            THROW 50003, 'No attraction with this AttractionID.', 1;

        -- Pobranie liczby miejsc zarezerwowanych na wycieczkę powiązaną z rezerwacją
        DECLARE @ReservedSpots INT;
        SELECT @ReservedSpots = Spots FROM Reservations WHERE ReservationID = @ReservationID;

        -- sprawdzenie dodanie TRIPID
        DECLARE @TripID INT;
        select @TripID = TripID from Reservations where ReservationID=@ReservationID;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripDate DATE;
        select @TripDate = StartDate from Trips where TripID=@TripID;

        -- sprawdzenie, czy jest wiecej na atrakcje niz na calego tripa
        IF @AttendeesNumber > @ReservedSpots
            THROW 50004, 'You cannot take more people to an attraction than the whole trip.', 1;

        IF DATEDIFF(DAY, getdate(), @TripDate) < 7
            THROW 50005, 'Cannot make reservation, time to do that have ended.', 1;

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50006, 'Reservation is not active.', 1;

        -- Pobranie liczby miejsc maksymalnych na atrakcji
        DECLARE @AllSpots INT;
        SELECT @AllSpots = Spots FROM Attractions WHERE AttractionID = @AttractionID;

        -- Pobranie liczby miejsc zarezerwowanych już dla tej atrakcji
        DECLARE @ReservedAttractionSpots INT;
        SELECT @ReservedAttractionSpots = ISNULL(SUM(AttendeesNumber), 0) 
        FROM ReservationDetails 
        WHERE AttractionID = @AttractionID and ReservationID not in (select ReservationID from Reservations where IsActive=0);

        -- Sprawdzenie, czy liczba miejsc jest git
        IF (@AllSpots - @ReservedAttractionSpots) < @AttendeesNumber
            THROW 50007, 'Not enough free spots for this attraction to book.', 1;

        -- Pobranie ceny atrakcji
        DECLARE @AttractionPrice DECIMAL(19, 2);
        SELECT @AttractionPrice = Price FROM Attractions WHERE AttractionID = @AttractionID;

        -- Dodanie szczegółów rezerwacji
        INSERT INTO ReservationDetails (ReservationID, AttractionID, AttendeesNumber, Price)
        VALUES (@ReservationID, @AttractionID, @AttendeesNumber, @AttractionPrice);

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad3](przyklady/procedures/addattrres.png)

## 4. Procedura wyświetlająca płatności w podanym okresie czasu
```sql
CREATE OR ALTER PROCEDURE p_get_payments_in_date_range
    @startDate DATE,
    @endDate DATE
AS
BEGIN

    SELECT 
        p.PaymentID,
        r.CustomerID,
        r.ReservationID,
        p.PaymentDate,
        p.Amount,
        p.PaymentMethod,
        CASE
            WHEN pc.CustomerID IS NOT NULL THEN CONCAT(pc.FirstName, ' ', pc.LastName)
            WHEN co.CustomerID IS NOT NULL THEN co.CompanyName
        END AS CustomerName
    FROM 
        Payments p
    INNER JOIN 
        Reservations r ON p.ReservationID = r.ReservationID
    INNER JOIN 
        Customers c ON r.CustomerID = c.CustomerID
    LEFT JOIN 
        PrivateClients pc ON r.CustomerID = pc.CustomerID
    LEFT JOIN 
        Companies co ON r.CustomerID = co.CustomerID
    WHERE 
        p.PaymentDate BETWEEN @startDate AND @endDate
    ORDER BY 
        p.PaymentDate;

END;
```
## Przykład użycia
![pprzyklad4](przyklady/procedures/getpaymentsindaterange.png)

## 5. Procedura dodająca gościa do atrakcji
```sql
CREATE OR ALTER PROCEDURE p_add_guest_attr
    @ReservationID INT,
    @AttractionID INT,
    @GuestID INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie czy ReservationID i AttractionID istnieją
        IF NOT EXISTS (SELECT * FROM Reservations WHERE ReservationID = @ReservationID)
            THROW 50001, 'No reservation with this ReservationID.', 1;
        
        IF NOT EXISTS (SELECT * FROM ReservationDetails WHERE AttractionID = @AttractionID and ReservationID = @ReservationID)
            THROW 50002, 'No attraction reserved with this AttractionID.', 1;

        IF NOT EXISTS (SELECT * FROM Guests WHERE GuestID = @GuestID)
            THROW 50003, 'No guest with this GuestID.', 1;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripID INT;
        select @TripID = TripID from Reservations where ReservationID=@ReservationID;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripDate DATE;
        select @TripDate = StartDate from Trips where TripID=@TripID;

        IF DATEDIFF(DAY, getdate(), @TripDate) < 7
            THROW 50004, 'Cannot add guest, it''s too late. :<', 1;

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50005, 'Reservation is not active.', 1;

        -- Pobranie liczby miejsc zarezerwowanych na atrakcję
        DECLARE @ReservedSpots INT;
        SELECT @ReservedSpots = AttendeesNumber 
        FROM ReservationDetails 
        WHERE ReservationID = @ReservationID AND AttractionID = @AttractionID;

        -- Obliczenie liczby gości przypisanych do tej rezerwacji atrakcji
        DECLARE @GuestCount INT;
        SELECT @GuestCount = COUNT(*) 
        FROM GuestDetails 
        WHERE ReservationID = @ReservationID AND AttractionID = @AttractionID;

        -- Sprawdzenie dostępnych miejsc na atrakcję
        IF @GuestCount >= @ReservedSpots
            THROW 50006, 'No available spots for this attraction.', 1;

        -- Dodanie nowego gościa do rezerwacji atrakcji
        INSERT INTO GuestDetails (GuestID, ReservationID, AttractionID)
        VALUES (@GuestID, @ReservationID, @AttractionID);

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad5](przyklady/procedures/addguestattr.png)

## 6. Procedura dodająca gościa do rezerwacji
```sql
create or ALTER PROCEDURE p_add_guest
    @ReservationID INT,
    @FirstName VARCHAR(50),
    @LastName VARCHAR(50)
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie czy ReservationID istnieje
        IF NOT EXISTS (SELECT * FROM Reservations WHERE ReservationID = @ReservationID)
            THROW 50001, 'No reservation with this ReservationID.', 1;

        -- Pobranie liczby miejsc zarezerwowanych w rezerwacji
        DECLARE @ReservedSpots INT;
        SELECT @ReservedSpots = Spots FROM Reservations WHERE ReservationID = @ReservationID;

        -- Obliczenie liczby gości przypisanych do rezerwacji
        DECLARE @GuestCount INT;
        SELECT @GuestCount = COUNT(*) FROM Guests WHERE ReservationID = @ReservationID;

        -- Sprawdzenie dostępnych miejsc
        IF @GuestCount >= @ReservedSpots
            THROW 50002, 'No available spots for this reservation.', 1;

        -- sprawdzenie dodanie TRIPID
        DECLARE @TripID INT;
        select @TripID = TripID from Reservations where ReservationID=@ReservationID;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripDate DATE;
        select @TripDate = StartDate from Trips where TripID=@TripID;

        IF DATEDIFF(DAY, getdate(), @TripDate) < 7
            THROW 50003, 'Cannot add guest, it''s too late. :<', 1;

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50004, 'Reservation is not active.', 1;

        -- Dodanie nowego gościa
        INSERT INTO Guests (ReservationID, FirstName, LastName)
        VALUES (@ReservationID, @FirstName, @LastName);

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad6](przyklady/procedures/addguest.png)

## 7. Procedura zmieniająca rezerwację
```sql
create or ALTER PROCEDURE p_alter_reservation
    @ReservationID INT,
    @CustomerID INT,
    @Spots INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION
        IF NOT EXISTS (SELECT * FROM Reservations WHERE ReservationID = @ReservationID)
            THROW 50001, 'No reservation with this ReservationID.', 1;

        DECLARE @TripID INT;
        SELECT @TripID = TripID FROM Reservations WHERE ReservationID = @ReservationID;
        DECLARE @TripSpots INT;
        SELECT @TripSpots = Spots FROM Trips WHERE TripID = @TripID;
        DECLARE @ReservedSpots INT;
        SELECT @ReservedSpots = ISNULL(SUM(Spots), 0) FROM Reservations WHERE TripID = @TripID and IsActive=1;
        DECLARE @ThisReservedSpots INT;
        SELECT @ThisReservedSpots = Spots FROM Reservations WHERE ReservationID = @ReservationID;
        IF @Spots > (@TripSpots - @ReservedSpots + @ThisReservedSpots)
            THROW 50002, 'Not enough available spots for this trip.', 1;

        DECLARE @GuestsAdded INT;
        SELECT @GuestsAdded = Count(GuestID) FROM Guests WHERE ReservationID = @ReservationID;

        IF @Spots > @GuestsAdded
            THROW 50003, 'There is more added guests than your desired number.', 1;

        declare @today date;
        select @today = getdate()

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50004, 'Reservation is not active.', 1;

        IF @today < (SELECT AvailableFrom FROM Trips WHERE TripID = @TripID)
            THROW 50005, 'You cannot edit a reservation for this trip yet. :(', 1;
        
        IF DATEDIFF(DAY, @today, (SELECT StartDate FROM Trips WHERE TripID = @TripID)) < 7
            THROW 50006, 'Time to edit reservations for this trip is over. :(', 1;

        DECLARE @TripPrice DECIMAL(19, 2);
        SELECT @TripPrice = Price FROM Trips WHERE TripID = @TripID;

        UPDATE Reservations set Spots=@Spots, ReservationDate=getdate(), Price=@TripPrice where ReservationID=@ReservationID

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad7](przyklady/procedures/alterreservation.png)

## 8. Procedura usuwająca gościa
```sql
create or ALTER PROCEDURE p_remove_guest
    @GuestID INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie czy GuestID, ReservationID i AttractionID istnieją
        IF NOT EXISTS (SELECT * FROM Guests WHERE GuestID = @GuestID)
            THROW 50001, 'No guest found with this GuestID.', 1;
        
        DECLARE @ReservationID INT;
        select @ReservationID=ReservationID from Guests

        -- sprawdzenie dodanie TRIPID
        DECLARE @TripID INT;
        select @TripID = TripID from Reservations where ReservationID=@ReservationID;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripDate DATE;
        select @TripDate = StartDate from Trips where TripID=@TripID;

        IF DATEDIFF(DAY, getdate(), @TripDate) < 7
            THROW 50002, 'Cannot remove guest, it''s too late. :<', 1;

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50003, 'Reservation is not active.', 1;

        -- Usunięcie gościa z tabeli GuestDetails
        DELETE FROM GuestDetails 
        WHERE GuestID = @GuestID;

        DELETE FROM Guests
        WHERE GuestID = @GuestID;

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad8](przyklady/procedures/removeguest.png)

## 9. Procedura usuwająca gościa z atrakcji
```sql
create or ALTER PROCEDURE p_remove_guest_attr
    @GuestID INT,
    @ReservationID INT,
    @AttractionID INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION

        -- Sprawdzenie czy GuestID, ReservationID i AttractionID istnieją
        IF NOT EXISTS (SELECT * FROM GuestDetails WHERE GuestID = @GuestID AND ReservationID = @ReservationID AND AttractionID = @AttractionID)
            THROW 50001, 'No guest found with this GuestID, ReservationID, and AttractionID.', 1;

        -- sprawdzenie dodanie TRIPID
        DECLARE @TripID INT;
        select @TripID = TripID from Reservations where ReservationID=@ReservationID;
        
        -- sprawdzenie dodanie TRIPID
        DECLARE @TripDate DATE;
        select @TripDate = StartDate from Trips where TripID=@TripID;

        IF DATEDIFF(DAY, getdate(), @TripDate) < 7
            THROW 50002, 'Cannot remove guest, it''s too late. :<', 1;

        IF (select Isactive from Reservations where ReservationID=@ReservationID) = 0
            THROW 50003, 'Reservation is not active.', 1;

        -- Usunięcie gościa z tabeli GuestDetails
        DELETE FROM GuestDetails 
        WHERE GuestID = @GuestID AND ReservationID = @ReservationID AND AttractionID = @AttractionID;

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
## Przykład użycia
![pprzyklad9](przyklady/procedures/removeguestattr.png)

## 10. Procedura usuwająca rezerwację
```sql
create or ALTER PROCEDURE p_remove_reservation
    @ReservationID INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION;

        IF NOT EXISTS (SELECT * FROM Reservations WHERE ReservationID = @ReservationID)
            THROW 50001, 'No reservation with this ReservationID. :(', 1;

        DECLARE @today DATE;
        SELECT @today = GETDATE();

        DECLARE @TripID INT;
        SELECT @TripID = (SELECT TripID FROM Reservations WHERE ReservationID=@ReservationID)

        IF DATEDIFF(DAY, @today, (SELECT StartDate FROM Trips WHERE TripID = @TripID)) < 7
            THROW 50004, 'Time to edit reservations for this trip is over. :(', 1;

        UPDATE Reservations SET IsActive = 0 WHERE ReservationID = @ReservationID;

        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```

## Przykład użycia
![pprzyklad10](przyklady/procedures/removereservation.png)

## 11. Procedura usuwająca rezerwacje nieopłacone, bądź bez listy gości (powinna wykonywać się co kilka godzin z pomocą agenta)
```sql
CREATE or ALTER PROCEDURE auto_p_check_reservations
AS
BEGIN
    BEGIN TRY
        -- Rozpocznij transakcję
        BEGIN TRANSACTION

        -- Utwórz tymczasową tabelę do przechowywania rezerwacji, których wycieczki zaczynają się za mniej niż 7 dni
        CREATE TABLE #UpcomingTrips (
            ReservationID INT,
            TripID INT,
            StartDate DATE
        );

        -- Wstaw dane do tymczasowej tabeli
        INSERT INTO #UpcomingTrips (ReservationID, TripID, StartDate)
        SELECT r.ReservationID, r.TripID, t.StartDate
        FROM Reservations r
        JOIN Trips t ON r.TripID = t.TripID
        WHERE DATEDIFF(DAY, GETDATE(), t.StartDate) < 7;

        -- Sprawdź nieopłacone rezerwacje i ustaw IsActive na 0
        UPDATE Reservations
        SET IsActive = 0
        WHERE ReservationID IN (
            SELECT ReservationID
            FROM dbo.PaymentsInfo
            WHERE LeftToPay > 0
              AND ReservationID IN (SELECT ReservationID FROM #UpcomingTrips)
        );

        -- Sprawdź liczbę gości vs liczbę miejsc i ustaw IsActive na 0
        UPDATE Reservations
        SET IsActive = 0
        WHERE ReservationID IN (
            SELECT r.ReservationID
            FROM Reservations r
            LEFT JOIN Guests g ON r.ReservationID = g.ReservationID
            GROUP BY r.ReservationID,r.Spots
            HAVING COUNT(g.GuestID) != r.Spots
              AND r.ReservationID IN (SELECT ReservationID FROM #UpcomingTrips)
        );

        -- Sprawdź liczbę uczestników vs liczbę miejsc w atrakcjach i ustaw IsActive na 0
        UPDATE Reservations
        SET IsActive = 0
        WHERE ReservationID IN (
            SELECT rd.ReservationID
            FROM ReservationDetails rd
            left JOIN GuestDetails gd ON rd.ReservationID = gd.ReservationID AND rd.AttractionID = gd.AttractionID
            GROUP BY rd.ReservationID, rd.AttractionID, rd.AttendeesNumber
            HAVING COUNT(gd.GuestID) != rd.AttendeesNumber
              AND rd.ReservationID IN (SELECT ReservationID FROM #UpcomingTrips)
        );

        -- Usuń tymczasową tabelę
        DROP TABLE #UpcomingTrips;

        -- Commit transakcji
        COMMIT;
    END TRY
    BEGIN CATCH
        IF XACT_STATE() <> 0
        BEGIN
            ROLLBACK TRANSACTION;
        END;
        THROW;
    END CATCH;
END;
```
