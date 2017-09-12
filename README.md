# meta

---
meta discussions / projects repository for mineral springs webapp development

this document is in progress of being written

---

# Jump List
* [Overview](#overview)
  * [main idea](#main-idea)
  * [how the architecture works](#how-the-architecture-works)
  * [roadmap](#roadmap)
  * [contributing and collaborating](#contributing-and-collaborating)
* **[Resources](#resource-list)**

# Overview

## main idea

Create a web-based application for Kennett High School's Mineral Springs Cafe

***Customers*** can easily place an order and see its price way ahead of time, and schedule a pickup.

***Cashiers*** can
* process paper or plastic payment at the point of sale with Square's Point of Sale Web API for iOS
* view currently waiting and previously served orders
* update the menu, from which people can order
* limit the service's availability to certain users, in case of abuse
* itemise transactions
* access statistics and periodic data about sales and revenue
* get live on-screen updates about new orders placed in real time

## how the architecture works

### frontend

* customers (***users***) can view the menu and create order placements linked to their Google account
* cashiers (***admins***) can manage and view transaction data, create and delete orders, modify the menu, view detailed information about an order, manage customer interaction, and process transactions in real-life through Square
---

* Graphical interface
* Hosted by Github Pages
* Cannot store or process data
  * Client-side JavaScript sends sanitised / minimally processed form data to the backend server
* Interfaces with Google Identity Platform and Square Point Of Sale Web API for iOS
* Data is processed from HTML input fields via JavaScript into JSON (pronounced "jason"), a notation for describing data, and sent to the backend server, along with some important metadata
  * time when the data was created, expressed in microseconds since 1 January 1970
  * (required for some data) a unique token, called an anti-csrf (anti-cross site request forgery) key or token, that ensures a certain level of data and use integrity
  * a verb that tells the processing code on both ends what the data relates to

### backend

* Stores all dynamic data -- lists of orders, lists of users, the menu, etc
* Hosted on a laptop on Cat's home wifi, served to the public with a tunnelled reverse proxy and secure DNS
* Creates and updates records of orders, payments, users, the current menu, etc
* Processes and validates requests and JSON data from the frontend
* Responsible for the Google Identity Platform sign-in and why it's secure
* Register and unregister anti-csrf tokens, to prevent unauthorised use of the service

## roadmap

where are we going?

## contributing and collaborating

working together

# Resource List

recommended resources / reading (list subject to additions):

### general
programming references
* search engine http://symbolhound.com http://google.co http://ddg.gg
* Stack Overflow https://stackoverflow.com
* **the commit logs, and the code itself**
  * https://github.com/mineralsprings/json-api-host
  * https://github.com/mineralsprings/mineralsprings.github.io
* Carter (Cat) Stevens, your omniscient lead developer

### web frontend
html5, css and js reference
* Mozilla Developer Network https://developer.mozilla.org
* W3Schools https://www.w3schools.com
* JSON https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON
* Bootstrap https://getbootstrap.com/docs/4.0/getting-started/introduction/ https://www.w3schools.com/bootstrap/
* jQuery (though we're not using it) https://learn.jquery.com/

### third-party apis / services
we're using a couple of 3rd-party apis to make stuff work -- learn about them.
* Google Identity Platform https://developers.google.com/identity/sign-in/web/
* Square Point of Sale Web API for iOS https://docs.connect.squareup.com/articles/web-api-ios
* OAuth2 (links to good resources) https://oauth.net/2/
* Github Pages https://github.io
* PageKite https://pagekite.me

### python backend
python 3 general and library references
* Python 3 https://docs.python.org/3/
* Requests https://python-requests.org
* AntiCSRF (written by Cat Stevens) https://codereview.stackexchange.com/q/165434
* HTTP/1.1 https://www.w3.org/Protocols/rfc2616/rfc2616.html
  * don't read the whole spec, but you should be able to skim it if you need to find something (Stack Overflow is also very good for this)
* most of the server is written in pure Python without other libraries, so **read the code** if you plan on working on it -- **it's very well commented**
