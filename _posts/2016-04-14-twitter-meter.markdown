---
layout: post
title:  "Twitter Meter Tutorial"
date:   2016-04-13 20:02:33 +0800
categories: tutorials
---


The web application's main purpose is to basically rate a candidate based on Twitter feeds about them. The application uses Twitter for Insights and Tone Analyzer service provided by IBM to get the emotion state of each feed. This app would be extremely useful for survey makers to help them create a more accurate sentiment of the people. With this application they will not have to interview hundreds of people but instead gather data via the internet. Further more, Twitter Meter can also help campaign managers in assessing how people feel about their campaign.

**Target Users**

- Survey makers
- Campaign Managers

**Deployement Instruction**

1. Create a folder in the **C:** directory. Name it anything you want.
2. Open a terminal and navigate to the newly created folder. Clone the git repository using the command : `git clone https://github.com/change-this/sample`.
3. Once finish, navigate through the directory using the command: `cd change-this/sample`.
4. To compile the application, enter the command: `gradle assemble`. This will create the `build/libs/myapp.war` file.
5. Upload it to Bluemix using the command: `cf push hackathon-RAD -m 512M -p build/libs/myapp.war`.

**End of Tutorial**

**Download powerpoint presentation [here][presentation].**

[presentation]: https://docs.google.com/presentation/d/1kIrXx_kfiLS1XsChy8P760Gim7DxGs6TQcWHTXvuUIU/edit#slide=id.g12b0134dac_5_0