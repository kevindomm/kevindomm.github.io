---
layout: post
title:  "Twitter for Insights and Tone Analyzer"
date:   2016-04-13 20:02:33 +0800
categories: tutorials
---

**Introduction**

The web application's main purpose is to basically rate a candidate based on Twitter feeds about them. The application uses Twitter for Insights and Tone Analyzer service provided by IBM to get the emotion state of each feed. This app would be extremely useful for survey makers to help them create a more accurate sentiment of the people. With this application they will not have to interview hundreds of people but instead gather data via the internet. Further more, Twitter Meter can also help campaign managers in assessing how people feel about their campaign.

**Target Users**

- Survey makers
- Campaign Managers

**Deployement Instruction**

1. Create the directory `TwitterMeter` in the root directory. 

2. Go to the created directory.

	```text
	> mkdir TwitterMeter
	> cd TwitterMeter
	```

3. Clone the github repository located [here.](wwww.google.com):

	```text
	> git clone https://github.com/<username>/<something>.git app
	```

4. Go to the `app` directory.

5. Compile the app by using Gradle's assemble task:

	```text
	> gradle assemble
	```

6. Login to your Bluemix Account.
	
	```text
	> cf login -a https://api.ng.bluemix.net -s dev
	```

6. Upload the newly created .war file to Bluemix using the command:

	```text
	> cf push hackathon-RAD -m 512M -p build/libs/myapp.war
	```

7. Go to the `DASHBOARD` of your Bluemix Account and go click the widget representing `hackathon-RAD`.

8. On the left pane, click the `Overview` link. 
	
9. Click the `ADD A SERVICE OR API` link.  You will be redirected to the `Catalog` page. 

10. Look for the `Insights for Twitter` service and click it.
 
11. Place the Application in the `dev` space.   

12. Connect it to the `hackathon-RAD` application. 

13. Click the `CREATE` button.

14. When asked to restage your application, DO NOT CLICK the `RESTAGE` button; cancel it, since you will still add another service. 

15. Similar to steps 7-13, add the Tone Analyzer service.

16. When asked to restage your application, click the `RESTAGE` button. 

17. Run the Application. 

**End of Tutorial**

**Download powerpoint presentation [here][presentation].**

[presentation]: https://github.com/kevindomm/Auto-Scaling/blob/master/autoscaling/Auto-Scaling.pptx?raw=true
