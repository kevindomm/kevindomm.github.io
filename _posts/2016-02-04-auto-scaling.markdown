---
layout: post
title:  "Auto-Scaling"
date:   2016-02-04 20:02:33 +0800
categories: tutorials
---
Auto-Scaling is a service offered by Bluemix that enables you to automatically add capacity to your application as needed. It also offers advance settings which makes its service more flexible.

<i>Gradle must be installed in your machine. Refer to sir Pantola's [Gradle Basics Tutorial][grdl-tut].</i>


##Deploying your web application##

1. Create a folder in the **C:** directory. It can be any name you want, but for this tutorial we'll be using **test**.
2. Open a terminal and navigate to the newly created folder. Clone the git repository using the command : `https://github.com/kevindomm/Auto-Scaling`.
3. Once finish, navigate through the directory using the command: `cd autoscaling/autoscaling`.
4. The cloned repository currently doesn't have a **build** folder which is required to run the application. To fix this, enter the command: `gradle assemble`. This will create the `build/libs/autoscalingapp.war` file.
5. Now that the app has been compiled, its time to upload it to Bluemix. To this, we enter the command: `cf push autoscaling-<username> -m 256M -p build/lib/autoscalingapp.war` where `<username>` is your own username.

The 256M was chosen because the app normally uses more than 128M and therefore crashes when uploaded using 128M.

##Manual Scaling##

1. To manually scale your newly created app, simply click the `DASHBOARD` from the menu.
2. Select your application.
3. Once you've done this, you will immediately see the `INSTANCES:` and `MEMORY QUOTA:`. These options are used to scale your application.

Adding an `INSTANCE` basically means you're adding a new machine to help your application run better. This is also known as horizontal scaling. Adding `MEMORY QUOTA` on the other hand, means you're only adding capacity per `INSTANCE`. This is known as vertical scaling.

##Binding Auto-Scaling to the Application##

1. Go to your app through the `DASHBOARD` from the menu.
2. Select `ADD A SERVICE OR API` and look for the Auto-Scaling service under **DevOps**.
3. Details of the service will be shown. Simply click the `CREATE` button. You will the have to restage your app after this step.
4. You will now have to create the Policy Configuration. Do this by clicking on `Auto-Scaling` under `SERVICES`.

	For this activity we'll be using the following settings:

		- Minimum Intance Count: 1
		- Maximum Intance Count: 3
		- Metric Type: Memory
		- Scale: Out: 65%, increase: 1
		- Scale: In: 40%, increase: 1

	Advance Configuration

		- Statistic Window: 30
		- Breach Duration: 60
		- Cooldown period for scaling out: 300
		- Cooldown period for scaling in: 300

	Most of the fields are self-explanatory except the following:

	- `Statistic Window`refers to the time period that the metric is measured.
	- `Breach Duration` indicates how long must the application exceed the upper threshold before adding a new instance.
	- `Cooldown periods` indicate how long the service will wait before it increases/decreases another instance.

5. Once you're done, click the `SAVE` button. You now have auto-scaling in your application.

##Testing the Auto-Scaling##

This part requires many users to access the application in order for it to overload and create another instance.

1. To simulate different users, we will be using a third party service called BlazeMeter. To do this simply go to `CATALOG` on the menu and look for BlazeMeter under **DevOps**.
2. Click the `CREATE` button.

	Unlike most services BlazeMeter cannot be bound to any application.

3. A link, `OPEN BLAZEMETER DASHBOARD`, will then appear in your screan. Click on it and you'll be redirected to the BlazeMeter website.
4. Once on the website, click the `Create Tests` found at the top bar and select `URL Test`.
5. Name the test anything you want and enter your app's URL under the `Enter request URL`.
	
	For this activity we'll be using the following settings and leave everything else in default:

	- Users: 50
	- Duration: 8
	- Uncheck the `SEND EMAIL ON REPORT END`

6. After clicking the `Save` button, A play(start) button will appear beside the test name. Click it and launch servers. It will take some time to prepare the servers.
7. While waiting, go back to your Bluemix tab and go to your application. Select the Auto-Scaling service and click the `Metric Statistics` tab. Once the test starts observe the data shown in the `Metric Statistics`.

Here you will see how the memory usage increases and suddenly decreases when a new instance is created. If you go to `Overview` now, you will see that the number of instances has increased. From the activty log you'll see the time the instance(s) was/were made and that it's the same time the graph went down from earlier.

[grdl-tut]: http://pong-pantola.github.io/gradle-basics/