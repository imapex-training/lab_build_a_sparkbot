# ToDo

* The Disect Section 
* Windows info
* Link for Kevin's Lab on Workstation Setup
* Prep for possiblity of DevNet Sandbox being down 
* Update with imapex branding

[item]: # (slide)

# Build a Spark Bot

Quickly get started with a functional Spark Bot, disect it's key components, and add cool new features.  


[item]: # (/slide)

[item]: # (slide)

# Pre-Reqs

* [Cisco Spark Account](http://ciscospark.com)
* [GitHub Account](https://github.com)
* [Docker Hub Account](https://hub.docker.com)
* Basic Workstation/Laptop Prep - **Link to Lab**

[item]: # (/slide)

[item]: # (slide)

## Cisco Spark Account

* [Cisco Spark](https://web.ciscospark.com)

![Cisco Spark](images/spark_newaccount.jpg)

[item]: # (/slide)

[item]: # (slide)

## GitHub Account

* [GitHub Account](https://github.com)

![GitHub](images/github_newaccount.jpg)

**Suggestion: Match your GitHub and Docker Hub Names (including case)**

[item]: # (/slide)

[item]: # (slide)

## Docker Hub Account

* [Docker Hub](https://hub.docker.com)

![Docker Hub](images/docker_newaccount.jpg)

**Suggestion: Match your GitHub and Docker Hub Names (including case)**

[item]: # (/slide)


[item]: # (slide)

## Basic Workstation/Laptop Prep

* Lab requires a Mac or Linux Environment
* Windows users can run the lab within a VM or Container ## ToDo - Add Windows info

[item]: # (/slide)

[item]: # (slide)

### Must have installed
* `git` command line tools - [Install Instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* `docker` daemon (Natively or *Docker for X*) - [Install Instructions](https://www.docker.com/products/overview)
* An IDE or Text Editor - [PyCharm Community Great Option](https://www.jetbrains.com/pycharm/download/) - **(not Notepad or TextEdit)**

[item]: # (/slide)

[item]: # (slide)

## Lab Phases 

* Deploy the Spark Bot Boilerplate (30 min)
* Disect the key elements of the Bot (40 min)
* Add a cool new feature (20 min)

[item]: # (/slide)

[item]: # (slide)

# Phase 1: Deploy the Spark Bot

1. Create a Bot Account in Spark
1. Setup bot code repository based on boilerplate
1. Build and Push initial Docker Image
1. Deploy your Bot
1. Test your Bot

[item]: # (/slide)

[item]: # (slide)

## Create Bot Account in Spark

A feature within Cisco Spark, is the ability to create *Bot* apps within an account.  Bots work nearly the same as full accounts with only a few differences.  Check this [page](https://developer.ciscospark.com/bots.html) for details. 

* Log into [developer.ciscospark.com](https://developer.ciscospark.com) with your own personal Spark account.  

[item]: # (/slide)

[item]: # (slide)

* Click on **My Apps** in the top menu

![](images/spark_myapps1.jpg)

[item]: # (/slide)

[item]: # (slide)

* Create a new **Bot** (do not create a new integration)

![](images/spark_newapp1.jpg)
	
[item]: # (/slide)

[item]: # (slide)

* **Bot Username** needs to be unique within Spark, and can **NOT** be changed

![](images/spark_newbot1.jpg)

**Sample Bot Image: [http://imapex.io/images/bot-avatar.jpg](http://imapex.io/images/bot-avatar.jpg)**
	
[item]: # (/slide)

[item]: # (slide)

* Record the *Access token* that is displayed on the next page, and **Save Changes**.  If you do NOT copy the token, you can regenerate it.  
* Also note the **Bot Username** that is displayed.  This is the ***Bot Email*** that will be needed when setting up your boilerplate code.  

[item]: # (/slide)

[item]: # (slide)

![](images/spark_newbot2.jpg)

[item]: # (/slide)

[item]: # (slide)

## Setup Bot Code Repository

We will leverage [github.com/imapex/boilerplate_sparkbot](https://github.com/imapex/boilerplate_sparkbot) as a starting point for our bot.  It was created to make it simple to get started with Bots by providing the needed foundation for a functioning bot and allow the developer to focus on new features.  

[item]: # (/slide)

[item]: # (slide)

* Download the setup script

```
# move to the directory where you store code for your projects
# DO NOT create a folder for your new bot
cd ~/coding 

# Download the script 
curl -OL https://github.com/imapex/boilerplate_sparkbot/raw/master/setup_and_install/new_bot_setup.sh

# Make the script executable 
chmod +x new_bot_setup.sh 
```

[item]: # (/slide)

[item]: # (slide)

###  The script will... 

* Download the boilerplate_sparkbot code
* Create a new local directory for your bot with the boilerplate code
* Delete the downloaded boilerplate code
* Create a new GitHub Repo on your account for the bot 
* Push up the boilerplate code to GitHub
 
[item]: # (/slide)

[item]: # (slide)

### Be Ready to provide... 

* Your GitHub Credentials
* A name for your new Spark Bot 
	* This will be used as the GitHub Repo Name
	* You'll want to use this same name for the Docker Repository you create later
	* Use no special characters, begin with a letter

[item]: # (/slide)

[item]: # (slide)

### NOTE regarding GitHub 2 Factor Auth

* If you have 2FA enabled on your GitHub account, you will need to provide a *Personal Access Token* when prompted for your password
* Tokens can be generated at [github.com/settings/tokens](https://github.com/settings/tokens)
* The token must have a minimum of `repo` access, and `delete_repo` access to automate the creation and cleanup of your new bot

[item]: # (/slide)

[item]: # (slide)

* Run the `new_bot_setup.sh` script

```
./new_bot_setup.sh
```

[item]: # (/slide)

[item]: # (slide)

## Build and Push Initial Docker Image

Our bot will be packaged and delivered as a Docker Image to provide ease of portability, dependency isolation, and simple updates and refreshes.  

[item]: # (/slide)

[item]: # (slide)

* You will need to have logged into Docker Hub on your workstation for this step.  If you haven't done so, you can by running: 

```
docker login 
```

[item]: # (/slide)

[item]: # (slide)

* Build the base bot

```
# Set a couple environment variables to make commands easier
# Replace the <NAME> with your data
export BOT_REPO=<GITHUB REPO>
export BOT_NAME=<YOUR BOT NAME>
export DOCKER_USER=<DOCKER HUB USERNAME>
    
# If you aren't in your new Git Repository directory, change into it 
cd $BOT_REPO
    
# Build a Docker image
docker build -t $DOCKER_USER/$BOT_REPO:latest .
```

[item]: # (/slide)

[item]: # (slide)

* Push the image to Docker Hub

```
docker push $DOCKER_USER/$BOT_REPO:latest
```

[item]: # (/slide)

[item]: # (slide)

## Deploy your Bot

These steps will deploy your bot to the Cisco DevNet Mantl Sandbox.  This is just one option that is freely available to use, however you can deploy your bot to any infrastructure that meets these requirements:

* Able to run a Docker Container
* Provides a URL for inbound access to running containers from the Internet
    * *Spark needs to be able to reach it with WebHooks*

[item]: # (/slide)

[item]: # (slide)

* Deploy your Bot.  
    
```
# From the root of your project... 
cd setup_and_install 
	
# Run the install script
./bot_install_sandbox.sh 
```
    
* Answer the questions asked

[item]: # (/slide)

[item]: # (slide)

* When complete, you should see a message that looks like this

```
Your bot is deployed to 

http://<DOCKER USERNAME>-<BOT NAME>.app.mantldevnetsandbox.com/
    
You should be able to send a message to yourself from the bot by using this call
    
curl http://<DOCKER USERNAME>-<BOT NAME>.app.mantldevnetsandbox.com/hello/<YOUR EMAIL ADDRESS>
    
You can also watch the progress from the GUI at: 
    
https://mantlsandbox.cisco.com/marathon
``` 

[item]: # (/slide)

[item]: # (slide)

## Test your Bot

Your Bot should now be running, let's verify it is up and working.  

[item]: # (/slide)

[item]: # (slide)

* Test that your bot is working by executing the `curl` command shown in your output.  If successfully deployed, you will recieve a message in Spark from your bot.   

```
curl http://<DOCKER USERNAME>-<BOT NAME>.app.mantldevnetsandbox.com/hello/<YOUR EMAIL ADDRESS>
```

[item]: # (/slide)

[item]: # (slide)

* Reply back to your bot and verify that the default commands are working.  
    * `/help` - should return a help message 
    * `/echo Spark Bots are Awesome!` - should reply back with `Spark Bots are Awesome!`

[item]: # (/slide)










[item]: # (slide)

# Phase 2: Disect the Bot

1. Webhooks
1. Building a REST API
1. Command Processing
1. Deploying and Running
1. Leveraging Cisco Spark in Code


[item]: # (/slide)

[item]: # (slide)

# Phase 3: Add a cool feature!

1. Add the command information 
1. Stub in your code for the feature
1. Update Bot Logic
1. Rebuild and Re-Deploy your Bot!

[item]: # (/slide)

[item]: # (slide)

## What feature to add you ask?

Have an idea, great!  If you need one...  

* How about Chuck Norris Jokes?
* Or Cat Facts? 

[item]: # (/slide)

[item]: # (slide)

## Bot Code File

The code for the bot is in the `bot.py` file located in the `bot` directory of the repository.  

```
$ tree
.
├── Dockerfile
├── LICENSE
├── README.md
├── bot
│   ├── bot.py
├── requirements.txt
└── setup_and_install
    ├── bot_install_sandbox.sh
    ├── bot_uninstall_sandbox.sh
    ├── new_bot_cleanup.sh
    ├── new_bot_setup.sh
    └── sample_marathon_app_def.json
```

Open this file in your IDE/text-editor

[item]: # (/slide)

[item]: # (slide)

## Chuck Norris via API

![Chuck Norris Database](http://icndb.com/wp-content/uploads/2011/01/icndb_logo2.png)

[http://icndb.com](http://icndb.com/)

[item]: # (/slide)

[item]: # (slide)

## Cat Facts Via API

[https://catfacts-api.appspot.com](https://catfacts-api.appspot.com/doc.html)

[item]: # (/slide)

[item]: # (slide)

## Add Command Information

Your bot listens for a specific set of commands to act on.  These are stored in a dictionary called `commands`.

* Add new commands to the command dictionary in bot/bot.py 

```
# The list of commands the bot listens for
# Each key in the dictionary is a command
# The value is the help message sent for the command
commands = {
    "/echo": "Reply back with the same message sent.",
    "/help": "Get help.", 
    "/chuck": "Get a random Chuck Norris Joke."
}
```

**Don't forget to add a comma after the entry for `help`**

[item]: # (/slide)

[item]: # (slide)

## Stub in Code for New Feature

Each command has a corresponding function that is called.  Here is the function for the `/echo` command.  

```
def send_echo(incoming):
    # Get sent message
    message = incoming["text"]
    # Slice first 6 characters to remove command
    message = message[6:]
    return message	
```

* Function **must** return the text of the message to be sent
* Passing the `incoming` data is only required if your command needs it

[item]: # (/slide)

[item]: # (slide)

## Sample Function

```
def chuck_joke():
    # Use urllib to get a random joke
    import urllib2
    
    response = urllib2.urlopen('http://api.icndb.com/jokes/random')
    joke = json.loads(response.read())["value"]["joke"]

    # Return the text of the joke
    return joke
```

[item]: # (/slide)


[item]: # (slide)

## Update Bot Logic

* Update the `if ...elif` section of the `process_incoming_message` function for your new command.  

```
# Some of function removed below
def process_incoming_message(post_data):
    # Take action based on command
    # If no command found, send help
    if command in ["","/help"]:
        reply = send_help(post_data)
    elif command in ["/echo"]:
        reply = send_echo(message)
    elif command in ["/chuck"]: 
        reply = chuck_joke()
	
    send_message_to_room(room_id, reply)	
```

[item]: # (/slide)

[item]: # (slide)

## Rebuild and Push Your Container

Our bot now has a new ability, but only on our laptop.  Now we must create a new Docker Image.

[item]: # (/slide)

[item]: # (slide)

* Build and Push a new Docker Image

```
# If you've opened a new terminal sense setting before
export BOT_REPO=<GITHUB REPO>
export BOT_NAME=<YOUR BOT NAME>
export DOCKER_USER=<DOCKER HUB USERNAME>

    
# Build a Docker image
docker build -t $DOCKER_USER/$BOT_REPO:latest .
docker push $DOCKER_USER/$BOT_REPO:latest
```

[item]: # (/slide)

[item]: # (slide)

## Restart Your Bot Application

We must restart our running bot to pull down and leverage the new container.  

* Login to Marathon at [https://mantlsandbox.cisco.com/marathon/](https://mantlsandbox.cisco.com/marathon/)
    * Username/Password: admin/1vtG@lw@y

[item]: # (/slide)

[item]: # (slide)

* Find your running Application.  It will be in a folder matching your Docker Username.  
 
![](images/sandbox_marathon1.jpg)

[item]: # (/slide)

[item]: # (slide)

* Click on your application, and then click **Restart**

![](images/sandbox_marathon2.jpg)

[item]: # (/slide)

[item]: # (slide)

* Wait until the new task shows as **Healthy** 
* Test your new command in Spark

[item]: # (/slide)
