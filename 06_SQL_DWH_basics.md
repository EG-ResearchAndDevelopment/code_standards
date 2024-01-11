# SQL DWH DW.Star basics

## 1. Introduction

A database warehouse usually consist of numerous DBs. The data here in our case is stored from different systems like technical,financal,personel,etc... Our DW.Star has mostly technical and customer data, which are allready filtered down through the ETL processes, but we still have some mistakes in there, like the summer time change has duplicate values and timestamps.

## 2. Basic understanding of the DB

Firstly we should understand that the database is seperated into 2 main categories:

- Technical Data (Dim tables)
- Measurements (Fact tables)

This means if we are looking for data with different timestamps we should use the tables FactKrivuljeNMC and FactKrivuljNapetostiNMC (voltages) in case we need the location or if the metering point is using solar power we should look into the table DimMerilnaMesta.

## 3. SOM vs. NMC tables

SOM tables indicate that the measurements are on the transformator level and NMC indicates Low voltage measurements. example:

- FactKrivuljeNMC will have measurements of metering points
- FactKrivuljeSOM will have measurements of transformator stations

In some cases we can also see DimDogodekStevec where stevec means metering point but we have a different table DimDogodekSOM for transformator stations events.

## 4. Understanding DimMerilnoMesto Table

First we need to know that we have about 91.000 - 92.000 metering points, but the table returns 600.000+ rows so let us take a look what is good to know here (similar practices apply to some other tables).

First let's take a look at **MerilnoMestoAktivno** which has a boolean Data type and tells us if the metering point is active:

    WHERE MerilnoMestoAktivno = 1 #verifies that the metering point is active

We have 2 columns MerilnoMestoSID and MerilnoMestoUID, MerilnoMestoSID is unique and is basically the contract ID. This tells us that MerilnoMestoUID can be in more rows under different MerilnoMestoSIDs. We can take a look under the column **veljavnost_spremembe_od** and **veljavnost_spremembe_do** to see if the contract is still valid:

    AND [veljavnost_spremembe_od] < GETDATE() #Validity of contract
    AND [veljavnost_spremembe_do] > GETDATE() #Validity of contract

Etl processes are also used beforehand on the data so we have to take this into account:

    AND EtlDeleted = 0   #Makes sure that rows is valid
    AND EtlInsertDate < GETDATE() #Check that the data inserted is older than the current date
    AND EtlUpdateDate < GETDATE() #Check that the data update is older than the current date

## 5. Querying

While executing queries in python we need to make sure that we close our connection after our query is done, thus we are avoiding memory leaks and comply with best practices which means we are not using additional resources to keep the connection, we can not lock the tables, security reasons and also taking into account that a DB has a limited simultaneous open connections:

        curr = con.cursor()
        query ="""
                    SELECT *
                    FROM DimMerilnaMesta"""
        out = curr.execute(query)
        data = out.fetchall()
        con.close()

In our database when querying for a specific timeframe it is best to use the index **DatumVeljavnostiCETID** since this will return a way faster result than for example DatumUraCET.

### 5.1 Joins

Joins here are not as usual practice through only ID-s from different tables but through names of the grid constants/devices like in the example IzovRazdelilca,PoljeCelica,RTP,... are using names in table which is used for the structure of metering points.

    StrukturaNMCSID	 SMM	IzvodRazdelilca	PoljeCelica    RTP	         TP	            KrajevnoNadzornistvo  PrikljucnaOmarica
    1	         1      IZV-R02         J20 ČIRČE      T0674 RTP LABORE  T0595 SMLEDNIŠKA   XXX - Nedefinirano	  PR_OM SMLEDNIŠKA CESTA 1

## 6. ETL-s (Extract, Transform and Load)

**ETL** stands for Extract, Transform, Load and it is a process used in data warehousing to extract data from various sources, transform it into a format suitable for loading into a data warehouse, and then load it into the warehouse. The process of ETL can be broken down into the following three stages:

- **Extract**: The first stage in the ETL process is to extract data from various sources such as transactional systems, spreadsheets, and flat files. This step involves reading data from the source systems and storing it in a staging area.
- **Transform**: In this stage, the extracted data is transformed into a format that is suitable for loading into the data warehouse. This may involve cleaning and validating the data, converting data types, combining data from multiple sources, and creating new data fields.
- **Load**: After the data is transformed, it is loaded into the data warehouse. This step involves creating the physical data structures and loading the data into the warehouse.
