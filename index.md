# Tables of Contents

* [About ICSBookMarket](#about-icsbookmarket)
* [Installation](#installation)
* [Application design](#application-design)
  * [Directory structure](#directory-structure)
  * [Import conventions](#import-conventions)
  * [Naming conventions](#naming-conventions)
  * [Data model](#data-model)
  * [CSS](#css)
  * [Routing](#routing)
  * [Authentication](#authentication)
  * [Authorization](#authorization)
  * [Configuration](#configuration)
  * [Quality Assurance](#quality-assurance)
    * [ESLint](#eslint)
    * [Data model unit tests](#data-model-unit-tests)
    * [JSDoc](#JSDoc)
* [Development History](#development-history)
  * [Milestone 1: Mockup Development](#milestone-1-mockup-development)
  * [Milestone 2: Data Model Development](#milestone-2-data-model-development)
  * [Milestone 3: Connect UI to data model](#milestone-3-connect-ui-to-data-model)

# UH Manoa Student Book Market for ICS Students

## About ICSBookMarket

The ICS Book Market allows the students of UHM to buy and sell books with each other. Buyers can search for books and message sellers to set up a transaction. Sellers can create listings for books they want to sell, and make it easy for buyers to contact them if they are interested in a book a seller has listed. What makes this application unique is that it's only available to the students of UHM and will be particularly useful for students within the ICS department or students who wish to learn material relevant to the ICS field of study. This application is exclusive to holders of myUH accounts.  Such localization may serve to avoid potential issues that buyers may be faced with when using other general or less specified markets to buy or sell products through.  


ICSBookMarket is a Meteor application providing a convenient way to buy and sell ICS textbooks amongst the University of Hawaii community. When you come to the site, you are greeted by the following landing page:

![](images/UHM-ICS-BM-Landing.png)

Anyone with a UH account can login to ICSBookMarket by clicking on the login button. The UH CAS authentication screen then appears and requests your UH account and password: 

![](images/UHM-ICS-BM-Login.png)

Once authenticated, you can look up books for sale or post your own books for sale. 

![](images/UHM-ICS-BM-Home.png)

The "Browse Books" option displays a list of all the textbooks required for ICS majors.

![](images/browse_books_2.png)

Selecting a particular textbook shows all posts that have that book up for sale.

![](images/book_check.png)

Students who want to post their textbooks for sale can fill out a form to specify the book, price, condition, and their contact information. 

![](images/UHM-ICS-BM-Sell-Books.png)

After a sale has been published, the user will be redirected to their books page, showing all the books they have up for sale. Users are able to edit books for sale or delete the post entirely if it has been sold.  

![](images/UHM-ICS-BM-Your-Books.png)

# Installation
First, [install Meteor](https://www.meteor.com/install).

Second, [download a copy of ICSBookMarket](https://github.com/icsbookmarket/icsbookmarket.git), or clone it using git.
  
Third, cd into the app/ directory and install libraries with:

```
$ meteor npm install
```
Fourth, add the image carousel with:

```
$ meteor add markoshust:owl-carousel-2
```

Fifth, run the system with:

```
$ meteor npm run start
```

# Development History

The development process for BowFolios conformed to [Issue Driven Project Management](http://courses.ics.hawaii.edu/ics314s17/modules/project-management/) practices. In a nutshell, development consists of a sequence of Milestones. Milestones consist of issues corresponding to 2-3 day tasks. GitHub projects are used to manage the processing of tasks during a milestone.  

The following sections document the development history of the UHM ICS BookMarket.

## Milestone 1: Mockup development

This milestone started on April 2, 2017 and ended on April 13, 2017.

The goal of Milestone 1 was to create a set of HTML pages providing a mockup of the pages in the system. To simplify things, the mockup was developed as a Meteor app. This meant that each page was a template and that FlowRouter was used to implement routing to the pages. 

Milestone 1 was implemented as [BowFolio GitHub Milestone M1](https://github.com/icsbookmarket/uhmicsbookmarket/milestone/1)

## Milestone 2: Data Model Development

This milestone started on April 14, 2017 and ended on April 25, 2017.

The goal of Milestone 2 was to implement the various collections needed for our application into the underlying Mongo database. We also set off to implement the UH CAS authentication system as well as improving the functionality of our app.

Milestone 2 was implemented as [BowFolio GitHub Milestone M2](https://github.com/icsbookmarket/uhmicsbookmarket/milestone/2)

The current deplyment of our application can be seen at [Meteor App Deployment](https://galaxy.meteor.com/app/uhmicsbookmarket.meteorapp.com)


