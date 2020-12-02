---
layout: post
title:  "Automated Feature Engineering Web App"
date:   2020-11-30
excerpt: "A Web app for feature engineering launched from command line"
project: true
tag:
- Flask web development
- MongoDB, HTML, JS, CSS, AJAX, JQuery
- Docker, Docker-compose
- Python package, setuptools
comments: true
---

CLICK HERE:
[Code repo](https://github.com/jeremite/auto-feature)

CLICK HERE:
[Full Medium Blog](https://jeremite.medium.com/automated-feature-engineering-web-app-using-flask-mongodb-docker-and-make-it-python-installable-6cb37387dec6)


## Overview
Normally feature engineering would take up to 80% of a Data Scientist's time and also involves many domain knowledge. The whole process is quite tedious and some similar tasks are repeated every time across different projects.
The web app I created free Data Scientist from the repeated coding and through some parameters definition in the User Interface, the features will be generated automatically for you, which would save estimated 80% of a Data Scientist's time.

Take user inputs like the tables (entities) will be used
![Web page sample](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/entity.png?raw=true)
The app will estimate features that allow user to adjust
![Web page sample2](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/output.png?raw=true)


## Challenges
1. How to modulize feature engineering components and reuse them effectively and efficiently
2. Dynamic selection and interactive tables
3. Make the app portable and easy to install


## Solutions
1. Took advantage of a third party package "featuretools" that take over the repeated tasks.
2. Used MongoDB to store the user input; JQuery+Ajax+Js to make table editable and interactive.
3. Leveraged two Docker to containerize the app and MongoDB, respectively and Docker-compose to organize them.

## Details
Since I've already written an article about it on Medium.com, **please check it out through the link above.**
