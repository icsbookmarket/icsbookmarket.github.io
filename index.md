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
Fourth, run the system with:

```
$ meteor npm run start
```

If all goes well, the application will appear at [http://localhost:3000](http://localhost:3000). If you have an account on the UH test CAS server, you can login.

# Application Design

## Directory structure

The top-level directory structure contains:

```
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```

This structure separates configuration files (such as the settings files) in the config/ directory from the actual Meteor application in the app/ directory.

The app/ directory has this top-level structure:

```
client/
  lib/           # holds Semantic UI files.
  head.html      # the <head>
  main.js        # import all the client-side html and js files. 

imports/
  api/           # Define collection processing code (client + server side)
    base/
    interest/
    profile/
  startup/       # Define code to run when system starts up (client-only, server-only)
    client/        
    server/        
  ui/
    components/  # templates that appear inside a page template.
    layouts/     # Layouts contain common elements to all pages (i.e. menubar and footer)
    pages/       # Pages are navigated to by FlowRouter routes.
    stylesheets/ # CSS customizations, if any.

node_modules/    # managed by Meteor

private/
  database/      # holds the JSON file used to initialize the database on startup.

public/          
  images/        # holds static images for landing page and predefined sample users.
  
server/
   main.js       # import all the server-side js files.
```

## Import conventions

This system adheres to the Meteor 1.4 guideline of putting all application code in the imports/ directory, and using client/main.js and server/main.js to import the code appropriate for the client and server in an appropriate order.

This system accomplishes client and server-side importing in a different manner than most Meteor sample applications. In this system, every imports/ subdirectory containing any Javascript or HTML files has a top-level index.js file that is responsible for importing all files in its associated directory.   

Then, client/main.js and server/main.js are responsible for importing all the directories containing code they need. For example, here is the contents of client/main.js:
```
import '/imports/startup/client';
import '/imports/startup/both';
import '/imports/api/stuff';
import '/imports/ui/layouts';
import '/imports/ui/components/form-controls';
import '/imports/ui/pages';
import '/imports/ui/stylesheets/style.css';
```
Apart from the last line that imports style.css directly, the other lines all invoke the index.js file in the specified directory.

We use this approach to make it more simple to understand what code is loaded and in what order, and to simplify debugging when some code or templates do not appear to be loaded.  In our approach, there are only two places to look for top-level imports: the main.js files in client/ and server/, and the index.js files in import subdirectories. 

Note that this two-level import structure ensures that all code and templates are loaded, but does not ensure that the symbols needed in a given file are accessible.  So, for example, a symbol bound to a collection still needs to be imported into any file that references it. 

## Naming conventions

This system adopts the following naming conventions:

  * Files and directories are named in all lowercase, with words separated by hyphens. Example: accounts-config.js
  * "Global" Javascript variables (such as collections) are capitalized. Example: Bookdata.
  * Other Javascript variables are camel-case. Example: bookdataList.
  * Templates representing pages are capitalized, with words separated by underscores. Example: Browse_Books_Page. The files for this template are lower case, with hyphens rather than underscore. Example: browse-books-page.html, browse-books-page.js.
  * Routes to pages are named the same as their corresponding page. Example: Browse_Books_Page.
  
## Data model

The ICSBookMarket data model is implemented by multiple Javascript classes

## CSS

Note that the user pages contain a menu fixed to the top of the page, and thus the body element needs to have padding attached to it.  However, the landing page does not have a menu, and thus no padding should be attached to the body element on that page. To accomplish this, the [router](https://github.com/icsbookmarket/uhmicsbookmarket/blob/master/app/imports/startup/client/router.js) uses "triggers" to add an remove the appropriate classes from the body element when a page is visited and then left by the user. 

## Routing

## Authentication

For authentication, the application uses the University of Hawaii CAS test server, and follows the approach shown in [meteor-example-uh-cas](http://ics-software-engineering.github.io/meteor-example-uh-cas/).

When the application is run, the CAS configuration information must be present in a configuration file such as  [config/settings.development.json](https://github.com/ics-software-engineering/meteor-application-template/blob/master/config/settings.development.json). 

Anyone with a UH account can login and use UHMICSBookMarket to create a portfolio.  A profile document is created for them if none already exists for that username.

## Authorization

## Configuration

## Quality Assurance

### ESLint

BowFolios includes a [.eslintrc](https://github.com/icsbookmarket/uhmicsbookmarket/blob/master/app/.eslintrc) file to define the coding style adhered to in this application. You can invoke ESLint from the command line as follows:

```
meteor npm run lint
```

ESLint should run without generating any errors.  

It's significantly easier to do development with ESLint integrated directly into your IDE (such as IntelliJ).

# Development History

The development process for UHMICSBookMarket conformed to [Issue Driven Project Management](http://courses.ics.hawaii.edu/ics314s17/modules/project-management/) practices. In a nutshell, development consists of a sequence of Milestones. Milestones consist of issues corresponding to 2-3 day tasks. GitHub projects are used to manage the processing of tasks during a milestone.  

The following sections document the development history of the UHM ICS BookMarket.

## Milestone 1: Mockup development

This milestone started on April 2, 2017 and ended on April 13, 2017.

The goal of Milestone 1 was to create a set of HTML pages providing a mockup of the pages in the system. To simplify things, the mockup was developed as a Meteor app. This meant that each page was a template and that FlowRouter was used to implement routing to the pages. 

Mockup for the following pages were implemented during M1:

<img width="200px" src="images/UHM-ICS-BM-Landing.png"/>
<img width="200px" src="images/UHM-ICS-BM-Login.png"/>
<img width="200px" src="images/UHM-ICS-BM-Home.png"/>
<img width="200px" src="images/browse_books_2.png"/>
<img width="200px" src="images/book_check.png"/>
<img width="200px" src="images/UHM-ICS-BM-Sell-Books.png"/>
<img width="200px" src="images/UHM-ICS-BM-Your-Books.png"/>

Milestone 1 was implemented as [UHMICSBookMarket GitHub Milestone M1](https://github.com/icsbookmarket/uhmicsbookmarket/milestone/1)

![](images/m1_network.png)

Milestone 1 consisted of five issues, and progress was managed via the [BowFolio GitHub Project M1](https://github.com/bowfolios/bowfolios/projects/1):

![](images/m1_issues.png)

Each issue was implemented in its own branch, and merged into master when completed:

![](images/m1_network.png)

## Milestone 2: Data Model Development

This milestone started on April 14, 2017 and ended on April 25, 2017.

The goal of Milestone 2 was to implement the various collections needed for our application into the underlying Mongo database. We also set off to implement the UH CAS authentication system as well as improving the functionality of our app.

Milestone 2 was implemented as [BowFolio GitHub Milestone M2](https://github.com/icsbookmarket/uhmicsbookmarket/milestone/2)

The current deplyment of our application can be seen at [Meteor App Deployment](https://galaxy.meteor.com/app/uhmicsbookmarket.meteorapp.com)


