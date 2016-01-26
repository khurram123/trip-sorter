#TRIP SORTER

### How to execute the code

Make sure you have [Composer](https://getcomposer.org/doc/00-intro.md#installation-nix) installed

Extract the ZIP file in the webroot of your web server, e.g. C:\wamp\www

Navigate to the trip-sorter directory.
```
cd trip-sorter
```

Install the PHP dependencies (phpunit, phpdoc) and generate the autoloading file.

```
composer install
```

Browse the package url via browser, It should output sorted list.


### Dependencies
- PHP 5.4


Files
----------------------------------------------
    doc
    └── [Documentation]
    src
    └── BoardingCards
    │   │  └── Common
    │   │  │    └── AbstractBoardingCard.php
    │   │  ├── AirportBusBoardingCard.php
    │   │  ├── FlightBoardingCard.php
    │   │  └── TrainBoardingCard.php
    │   └── Utils
    │         └── Interfaces
    │         │     └── SortInterface.php
    │         └── Sorters
    │              └── TripSorter.php
     test
     └── AirportBusBoardingCardTest.php
     ├── FlightBoardingCardTest.php
     ├── TrainBoardingCardTest.php
     └── TripTest.php


### Extending class
* You can create new type of cards like plane, train, bus or whatever you want by extending the AbstractBoardingCard.


## Dev Stack Used

WAMP with PHP 5.5.9

- PhpStorm 10
- Terminal for php cli (Used html based output so CLI won't be clean and practically useless in test)
- php doc for documentation
- composer for getting phpdoc


## Understanding/ Methodology

- Regular OOP based PHP is used for creating the API. 
- I have kept the testing simple. 
- The boarding passes/cards have this following common info so a generic pass consists of:
	- Departure Location
	- Arrival Location
	- Seat
- A train, plane, airport, airport bus or any other terminal boarding passes have additional info that is the respective train #, flight #, bus #, terminal #, Gate # etc. This means is one super object for the boarding pass and for the bus, plane, train, airport bus etc, there is additional info with the respective detail.
- Since there is extra info pertaining to each class, on top of a boarding pass class, this enables me to make a base class and use DRY principle to inherit other kinds of passes from it.
- After creating the respective classes, each class can be used to create a boarding bass of certain type all inheriting from the base class.
- Another class is TripSorter which gets an object consisting of multiple objects with each being from one type of boarding pass objects (Train, Flight, Airport etc). So it takes these are sorts them.
- A trip class consists of n number of boarding passes of various types. It creates a TripSorter object and then uses a sorting method from TripSorter to get the same object with sorted boarding passes.


## I admit

- My focus had been more on the 'ability to deliver an appropriate, simple solution to the problem' than actually working on organizing the code. I tried though!
- There are three steps in the sorting alo each of O(n) = 3n.
