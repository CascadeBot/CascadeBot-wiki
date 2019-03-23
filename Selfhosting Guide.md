## Selfhosting CascadeBot

At CascadeBot, we support individuals who decide to selfhost their version of our bot. Here you can find a guide to help you through selfhosting our bot.

This guide assumes that you have some knowledge in using databases, and have a Ubuntu 18.01 (Server Edition) server available to use.

#### Step 1 (Creating a database)

To host CascadeBot, you will need to have a MongoDB cluster for the bot to store information. We use MongoDB because its non-relational data structure makes it easy for our constantly evolving dataset.

We recommend that you use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) as it has a free tier option, which is good for a smaller instance to start out.

Once you've created an account with MongoDB Atlas and navigated to your "dashboard", click on the **Build a New Cluster** button. For this tutorial, I will be using the Google Cloud Platform provider, and the Belgium region. Mine looks [like this](images/database1.png). There's no need to change any other settings or options at this point, so just go ahead and click **Create Cluster**. New clusters usually take 5-10 minutes to become ready, so don't worry if the process appears to have hanged.

When the cluster has been created, select the **Security > IP Whitelist** tab and select **Add IP Address**. You're going to need the __External IP__ address of the Ubuntu server that you will be running your server on. Once you've got this, pop that IP into the "Whitelist Entry" box. You can enter a comment such as "Ubuntu Server" into the Comment box. Now you can go ahead and click confirm.

And now you've created your cluster! Keep this page open, we'll be needing it again later.

#### Step 2 (Getting the latest JAR file)

The CascadeBot team uses Jenkins to automatically build our changes, and push them into a JAR file. You can find our Jenkins page [**here**](https://jenkins.weeryan17.com/job/Cascade%20Bot/). You're going to want to download the `config.example.yml` and `CascadeBot-jar-with-dependencies.jar` files. Once downloaded, pop them onto your Ubuntu server via FTP.

#### Step 3 (Installing Java)

Of course, to run the CascadeBot JAR file you're going to need JDK 11 on your server. To install this, you're going to need to SSH into your server and run a few basic commands. 

First of all, you're just going to want to run `sudo apt-get update` and `sudo apt-get upgrade` on your server.

After this, you're going to need to run `sudo add-apt-repository ppa:linuxuprising/java` to add the PPA. Now, run `sudo apt-get install oracle-java11-installer` to get thee Java installer.

Once you've run the command to download the installer, a license agreement page will pop up. Press Tab to highlight the OK button, and hit Enter to accept it. I assume here that Java 11 is the only version of Java installed on your system.

Give the system a second to finish the install, and then run `java -version`. If it prints something like `java version "11.0.2" 2019-01-15 LTS
` then you're good.

#### Step 4 (Creating a Discord Bot user)

For the bot to be able to interface with users on Discord, you're going to need a bot user. This is the "account" that you can add to servers, and your bot will work from this.

Head over to the [Discord Developer Portal](https://discordapp.com/developers/applications/), and hit **New Application**. Give it a cool name and click **Create**. Once you've done this, click **Bot** on the left-nav bar and click **Add Bot** under Build-A-Bot. Choose a cool icon, or leave it as the default one!

You're going to need the Token which is visible on this page, and the Client ID which is visible on the **General Information** page. Keep this safe (and private!), you're going to need them for the next step.

#### Step 5 (The Configuration File)

Remember that `config.example.yml` file that we uploaded to the server earlier? We're going to need that again! Open it up on your local PC and rename it to `config.yml`. You're going to need to make some important changes here, so listen closely!

First thing you're going to need to do is paste in the Client ID and Bot Token that you created in the previous step. Make sure that the token is in the little quote marks, as these are necessary.

Next, you're going to need to add the MongoDB Atlas information. In this tutorial I am going to be using the `connection_string` option, as this is easier and is supported by MongoDB.

Comment out all of the other database options (username, password, database, hosts and ssl), and uncomment `connection_string`. Now we're going to head back over to the MongoDB Atlas page and get our connection string.

Once there, click **Connect** in your Cluster's card, and then click **Connect your Application**. You will then be given a Connection String, which you can copy and paste into your configuration file. You'll need to replace `<password>` with your MongoDB password.

You can either fill out the `official_server` option with "-1" or with your own server ID, depending on whether you want to use security roles (such as owners and moderators) or not. Filling out all of the role IDs is optional, but if you don't fill them in then nobody will be able to run the developer commands such as shutdown, eval and more.

For the `global_emotes` option, you can either create your own emoji assets or just leave them blank. Leaving them blank is fine, and isn't really very noticeable when using the bot.

You'll need to put two double quotes ("") in the `secret_key` section.

Once you've done all of this, save the file and upload it to the same directory as the CascadeBot JAR file.

#### Step 6 (The Final Step!)

Congratulations for getting this far! You're now (in theory) ready to start up the bot and invite it to guilds. 

SSH into your server and navigate to the directory in which you've been uploading the CascadeBot files. Once there, run `java -jar CascadeBot-jar-with-dependencies.jar` and your bot will boot up.

To invite the bot to servers, use this link: `https://discordapp.com/oauth2/authorize?client_id=[REPLACE]&scope=bot&permissions=0` and replace the obvious text with your Client ID, found on the Discord Developer Portal.

### Thanks for reading!

If you need any extra support, please join the CascadeBot Official Discord at [INSERT LINK]. I hope you found this tutorial helpful!