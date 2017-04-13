# Tables of Contents

* [About ICSBookMarket](#about-icsbookmarket)
* [Installation](#installation)
* [Development History](#development-history)
  * [Milestone 1: Mockup Development](#milestone-1-mockup-development)
  * [Milestone 2: Data Model Development](#milestone-2-data-model-development)

# UH Manoa Student Book Market for ICS Students

## About ICSBookMarket

The ICS Book Market allows the students of UHM to buy and sell books with each other. Buyers can search for books and message sellers to set up a transaction. Sellers can create listings for books they want to sell, and make it easy for buyers to contact them if they are interested in a book a seller has listed. What makes this application unique is that it's only available to the students of UHM and will be particularly useful for students within the ICS department or students who wish to learn material relevant to the ICS field of study. This application is exclusive to holders of myUH accounts.  Such localization may serve to avoid potential issues that buyers may be faced with when using other general or less specified markets to buy or sell products through.  

## Landing Page

Landing Page has a short description/overview of the website.

<img class="ui image" src="/images/UHM-ICS-BM-Landing.png">

## Login Page 

<img class="ui image" src="/images/UHM-ICS-BM-Login.png">

## Home Page

<img class="ui image" src="/images/UHM-ICS-BM-Home.png">

## Browse Books Page

Displays a list of all the textbooks required in ICS major.

<img class="ui image" src="/images/browse_books.png">

## Sell Books Page

Submit seller information and book details.

<img class="ui image" src="/images/UHM-ICS-BM-Sell-Books.png">

## Your Books Page

Shows all the books you put up for sale

<img class="ui image" src="/images/UHM-ICS-BM-Your-Books.png">

## Book Check Page

Shows a table with list of people who are selling the selected textbook.

<img class="ui image" src="/images/book_check.png">


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

## Milestone 2: Data Model Development

This milestone started on April 14, 2017 and ended on April 25, 2017.

The goal of Milestone 2 was to implement the various collections needed for our application into the underlying Mongo database. We also set off to implement the UH CAS authentication system as well as improving the functionality of our app.
