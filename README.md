# NodeJSCloudantSampleApp Overview

This application uses CloudantNoSQL database service to demonstrate the operations of Create, Read, Update and Delete into database, using Node.js runtime. Cloudant node module is used for these operations. They can alternatively be done with API calls which returns a JSON.

### ** Click on the button below to deploy this Bluemix project to your account **

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://hub.jazz.net/git/neerajaganesan/NodeJSCloudantSampleApp)


## Application Requirements

* NodeJS runtime
* CloudantNoSQLDatabase service

## Running the app on Bluemix

1. [Sign up][sign_up] for Bluemix.
2. Download and install Cloud Foundry CLI to be used on the terminal.
3. Fork this project into your Bluemix account by clickig on the "Fork Project" button in the top-right hand corner of this page : https://hub.jazz.net/git/neerajaganesan/NodeJSCloudantSampleApp
4. On the Terminal, Connect to Bluemix using the CF CLI and follow the prompts to log in.
			$cf api https://api.ng.bluemix.net
			$cf login
4. Once you're in the same space as the app, create the CloudantNoSQLDB service in Bluemix
			$cf create-service cloudantNoSQLDB Shared <service-name>
5. Bind this service to your app:
			$cf bs NodeJSCloudantSampleApp <service-name-as-in-step-4>
6. Edit the manifest.yml file and change the <application-host> parameter to something unique.
		applications:
		- path: .
		  name: NodeJSCloudantSampleApp
		  host: <change_to_something_unique>
		  framework: node
		  memory:256M
		  instances: 1
		  services:
  			- <service-name-as-in-step-4>
   The host you use will determinate your application url(e.g. <host>.mybluemix.net). REMOVE the following lines from manifest.yml as you no longer need this cloudant service. The one you created in step 4 will be the one primarily used.
		declared-services:
  	    cloudant-nodejs:
    		label: cloudantNoSQLDB
    		plan: Shared
7. Start the application by typing
		$cf start NodeJSCloudantSampleApp

And voila! Your very own instance of CloudantNoSQLDB with NodeJSCloudantSampleApp is now running on Bluemix.

## Running the app locally:

1. If you have not already, download node.js and install it on your local machine.
2. Download the project to your local machine from this link : https://hub.jazz.net/git/neerajaganesan/NodeJSCloudantSampleApp
3. On Bluemix Dashboard, create CloudantNoSQLDB service if it's not alredy present.
4. Click on the service to open it in a new page. Click on "Service Credentials" in the left pane. Note value of "url".
5. On terminal, 'cd' into folder.
6. Copy "url" from step 4 into app.js of your project present in a local respository.
   Paste url in line 13 of app.js.
		cloudant_url = "<paste 'url' here>"
   Comment out lines 20-28
		/*
			if(process.env.VCAP_SERVICES)
			{
				services = JSON.parse(process.env.VCAP_SERVICES);
				if(services.cloudantNoSQLDB) //Check if cloudantNoSQLDB service is bound to your project
				{
					cloudant_url = services.cloudantNoSQLDB[0].credentials.url;  //Get URL and other paramters
					console.log("Name = " + services.cloudantNoSQLDB[0].name);
					console.log("URL = " + services.cloudantNoSQLDB[0].credentials.url);
    				console.log("username = " + services.cloudantNoSQLDB[0].credentials.username);
					console.log("password = " + services.cloudantNoSQLDB[0].credentials.password);
				}
			}
 		*/
8. cd into the project folder and if required by any modules, run
		npm install
6. Start the application by typing
		node app.js
7. When the application executes, the first line will say:
		http://localhost:<port_number>
Paste this URL in the browser to open the application.

### For more documents on CloudantNoSQLDB

* https://cloudant.com

* https://docs.cloudant.com/document.html#undefined

* https://github.com/cloudant/nodejs-cloudant/blob/master/example/crud.js

* https://www.ng.bluemix.net/docs/#services/Cloudant/index.html#Cloudant


## Troubleshooting

To troubleshoot your Bluemix app the main useful source of information are the logs, to see them, run:

  ```sh
  $ cf logs <application-name> --recent
  ```

## License

  This sample code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).
  This sample uses [socket.io](http://socket.io/) which is MIT license
## Contributing

  See [CONTRIBUTING](CONTRIBUTING.md).

## Open Source @ IBM
  Find more open source projects on the [IBM Github Page](http://ibm.github.io/)

[service_url]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/speech-to-text.html
[cloud_foundry]: https://github.com/cloudfoundry/cli
[getting_started]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/getting_started/
[sign_up]: https://apps.admin.ibmcloud.com/manage/trial/bluemix.html?cm_mmc=WatsonDeveloperCloud-_-LandingSiteGetStarted-_-x-_-CreateAnAccountOnBluemixCLI