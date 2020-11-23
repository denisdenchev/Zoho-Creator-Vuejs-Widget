# Zoho-Creator-Vuejs-Widget
Feeling Wobby - Dobby Creative?
Let's build a Creator Widget


1. Make a hot brew.

2. Tell your misses you are off on a mission.

3. Download and install Nodejs

- Download from here: "https://nodejs.org/en/download/"

4. After instalation of Node we have to make sure we have it installed and running. To do so press windows key + r or type "cmd" in the search and open it up. Once you have done that you can run this command  ( node-v ) this will tell you the version of your Nodejs.

1111.png

5. Once we have installed node we have nearly quialified to a Senior Developer Position.

6. Now we have to install the Zoho Extension Toolkit (ZET)
-  npm install -g zoho-extension-toolkit
Once we have done that the following screen would appear.
1112.png

7. Let's make sure we have ZET installed correctly.
In your cmd / CLI run the following command 
- zet
The following screen would appear
1113.png

Now as we have installed Nodejs and ZET, lets get another brew and create a project


Create a Project:
1. Using CLI navigate to the desired destination, where you would like to store your widget / application.
To move between folders you can use the command "cd folderName" and to move back out of that folder use "cd .."
1114.png

2. As we have masterted travelling back and forth in future, let's run the command to create a new project.
- In your terminal, in the desired location(folder) run  "zet init" to initialise ZET.
3.  A list of Zoho Services will be displayed.
- Select Creator and press Enter
1115.png

4. Now give your project a name and hit Enter

1115.png

5. The project has been created. Now navigate to it using cd.

1116.png

6. Using "zet run" command will start a local server on your machine, which you would use for development.
- After navigating to the folder of your project you can type "zet run" in your CLI and  voalá, you have a server, running locally on your machine.

1118.png

a. Type your IP address and the port in the web-browser. From there navigate to your "widget.html" file.

1119.png

b. And you would see the content of your "widget.html" file.

1120.png



7. Open up the project folder with whatever text editor you are using. I am using VS Code, if you are not... I feel sorry for you...
Go into App folder and find the "widget.html" file.
1117.png

8. Do your magic, using HTML, CSS  and JavaScript.

Here is a quick example:

1121.png

and the Output 



Do not forget to include the creator SDK in your html file
 -> <script src="https://js.zohostatic.com/creator/widgets/version/1.0/widgetsdk-min.js"></script>


1122.png

Now go and play with the button, it's good fun.


Let's say we are done with the first phase of developing our widget. Let's now host it with Zoho Creator and see it working.


1. To do so we have to validate and pack what we have just done.

- Go to your CLI and run "zet validate". If your server is still running in your CLI you can hit "Ctrl + C" and it will ask you if you would like to cancel and then type "Y" for yes.

1123.png

2. Type "zet validate" in the CLI

3. Type "zet pack" in the CLI

1124.png

These commands work as follows

zet validate - it validates your code and checks for errors or incompatible usability.

zet pack - it literally packs your files in a ".zip" file, which we would need to upload in a bit.



4. Upload your files to Zoho Creator.

- In your Zoho Creator you need to create a Page ( Widgets can only be used within pages and not forms).

- Edit application -> Open Page Builder 
1125.png



- Go to Widgets and create new

Screenshot - 2020-11-23T122841.278.png




Screenshot - 2020-11-23T123048.368.png

Give your widget a name

Set the hosting as "Internal".

Go to your project's folder -> Dist folder and choose the zip file (widget_tutorial.zip).

And under Index File write /widget.html.

Click on Create.

5. Once your widget has been created simply drag and drop it onto the page.

Done.
Screenshot - 2020-11-23T135024.201.png



Host your widget Externally and use it with Zoho Creator
1. Host your widget anywhere, that is not a local server.

2. Create your Widget 

Screenshot - 2020-11-23T141750.406.png

Give it a name and URL where your widget is hosted.

3. Job done!



This is how to create a simple widget, without doing any data manipulation with Zoho Creator records.


Let's talk about data manipulaiton


1. Get a how brew.

2. Create a form / report with some fields. See image below for example of the form I have created.

1126.png

- As you can see I want to populate these fields with the data that I have filled in.

Address, Name, Job Title, Date Of Birth ect...

You would need to structure a json-like data, depending on how the data in your report is structured.

3. Remember to ALWAYS initialise Zoho.Creator.

4. Choose the form/report you would like to add a record to
- In my case "Register Form".
5. Use ZOHO.CREATOR.API.addRecord() with the "data" object created above, to add record to a form.


Fetch data from report
1. Grab a beer (as it's 17:25 and you are finishing in a minute)

2. Use the simple code below to fetch data from the report you would like.

1127.png

3. Simply create a config object to set the parameters you would like in order to fetch a report. There are more parameters such as number of records to be fetched, number of pages to be fetched, records that are only active, inactive, ect...
- See zoho Docs for more information -> https://www.zoho.com/creator/newhelp/app-settings/widgets/creator-api-for-widgets.html

4. Fetch the records from the chosen report and you can manipulate the data as you wish.

5. Clock off.

6. Spend another 4 hours working on the widget as you enjoy it so much.





Zoho Creator - JavaScript Widget, using VueJS CDN


Set up your project, following the steps above. Only little alterations would be needed so we can actually use Vuejs components in our application.


1. Your main .html file should look like this:

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<meta name="viewport" content="width=device-width,initial-scale=1.0" />
<title>test widget</title>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12"></script>
<script src="https://unpkg.com/http-vue-loader"></script>
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://js.zohostatic.com/creator/widgets/version/1.0/widgetsdk-min.js"></script>
</head>
<body>
<noscript>
<strong
>We're sorry but test widget doesn't work properly without JavaScript
enabled. Please enable it to continue.</strong
>
</noscript>
<div id="app">
<root></root>
</div>
<script>
new Vue({
el: '#app',
components: {
root: httpVueLoader('./components/root.vue'),
},
});
</script>
</body>
</html>


2. Here we are initialising Vuejs via CDN and creating a new instance of Vuejs and we are attaching it to the tag with an ID of "app", we are also loading the component, using httpVueLoader.

3. We have set up our main Vuejs file to be called "root", this file is the bridge between plain " .html " file and the Vuejs components.

4. Here is how my root component looks like

<template>
  <div>
    <submit></submit>
  </div>
</template>
<script>
module.exports = {
  name: 'root',
  props: {
  },
  components: {
    'submit': httpVueLoader('./submit.vue')
  },
  data: () => {
    return {
      
    }
  }
}
</script>
<style scoped>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>


5. Here is how my "Submit" component lookis like
- I am only going to show you how to mount / import components into another components/containers
<script>
module.exports = {
  name: 'submit',
  props: {
  },
  components: {
    'field': httpVueLoader('./field.vue'),
    'emailfield': httpVueLoader('./emailfield.vue'),
    'mobilefield': httpVueLoader('./mobilefield.vue'),
    'submitbutton': httpVueLoader('./submitbutton.vue'),
  }
</script>


6. Let's whitelist some of the URL's we are using in our .html file, in order for Zoho Creator to accept them

- This is the "plugin-manifest.json" file

{
  "service": "CREATOR",
  "cspDomains": {
    "connect-src": [
      "https://cdn.jsdelivr.net",
      "https://unpkg.com",
      "https://127.0.0.1:5000"
    ]
  }
}


7. Again, once you are done with building your widget, do not forget to run "zet validate" and "zet pack" to update the .zip file you are going to upload and upload it again. 

Currently Zoho Creator does not work with html + Vuejs via CDN and we are awaiting on a response from Zoho in order to understand why. You can simply host your files somewhere free and use the Widget via it's URL.
You can also host locally your widget, for development purposes, it's quick and effective, make a change in your code and refresh the page.
