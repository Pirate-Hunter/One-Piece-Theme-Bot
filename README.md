![OnePieceBot](https://telegra.ph/file/1f012aed1a79aed2b1d68.jpg)
# One Piece Themed Group Management Bot

This bot is created exclusively for one piece communities & fans, an entirely themed persona to make One Piece Themed Bot suitable for Anime and Manga group chats. 

Can be found on telegram as [Monkey D. Luffy](http://t.me/Strawhat_Luffy_Robot).

The Support group and One Piece Community can be reached out to at [One Piece Base](https://t.me/OnePieceBase), where you can ask for help about [One Piece Bot](http://t.me/Strawhat_Luffy_Robot), discover/request new features, report bugs, and stay in the loop whenever a new update is available. 

News channel as at [One Piece Bot Updates](https://t.me/OnePieceUpdates) 


## How to setup/deploy.

### Read these notes carefully before proceeding 
 - Edit any mentions of @OnePieceBase to your own support chat. 
 - Your code must be open source and a link to your fork's repository must be there in the start reply of the bot. 
 - Lastly, if you are found to run this repo without the code being open sourced or the repository link not mentioned in the bot, we will push a gban for you in our network because of being in violation of the license, you are free to be a dick and not respect the open source code (we do not mind) but we will not be having you around our chats.


<details>
  <summary>Steps to deploy on Heroku !! </summary>

```
Fill in all the details, Deploy!
Now go to https://dashboard.heroku.com/apps/(app-name)/resources ( Replace (app-name) with your app name )
REMEMBER: Turn on worker dyno (Don't worry It's free :D) & Webhook
Now send the bot /start, If it doesn't respond go to https://dashboard.heroku.com/apps/(app-name)/settings and remove webhook and port.
```

  [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/Pirate-Hunter/One-Piece-Theme-Bot.git)

</details>  
<details>
  <summary>Steps to self Host!! </summary>

  ## Setting up the bot (Read this before trying to use!):
Please make sure to use python3.6, as I cannot guarantee everything will work as expected on older Python versions!
This is because markdown parsing is done by iterating through a dict, which is ordered by default in 3.6.

  ### Configuration

There are two possible ways of configuring your bot: a config.py file, or ENV variables.

The preferred version is to use a `config.py` file, as it makes it easier to see all your settings grouped together.
This file should be placed in your `OnePieceBot` folder, alongside the `__main__.py` file. 
This is where your bot token will be loaded from, as well as your database URI (if you're using a database), and most of 
your other settings.

It is recommended to import sample_config and extend the Config class, as this will ensure your config contains all 
defaults set in the sample_config, hence making it easier to upgrade.

An example `config.py` file could be:
```
from OnePieceBot.sample_config import Config

class Development(Config):
    OWNER_ID = 254318997  # your telegram ID
    OWNER_USERNAME = "SonOfLars"  # your telegram username
    API_KEY = "your bot api key"  # your api key, as provided by the @botfather
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # sample db credentials
    JOIN_LOGGER = '-1234567890' # some group chat that your bot is a member of
    USE_JOIN_LOGGER = True
    SUDO_USERS = [18673980, 83489514]  # List of id's for users which have sudo access to the bot.
    LOAD = []
    NO_LOAD = ['translation']
```

If you can't have a config.py file (EG on Heroku), it is also possible to use environment variables.
The following env variables are supported:
 - `ENV`: Setting this to ANYTHING will enable env variables

 - `TOKEN`: Your bot token, as a string.
 - `OWNER_ID`: An integer of consisting of your owner ID
 - `OWNER_USERNAME`: Your username

 - `DATABASE_URL`: Your database URL
 - `JOIN_LOGGER`: optional: a chat where your replied saved messages are stored, to stop people deleting their old 
 - `LOAD`: Space-separated list of modules you would like to load
 - `NO_LOAD`: Space-separated list of modules you would like NOT to load
 - `WEBHOOK`: Setting this to ANYTHING will enable webhooks when in env mode
 messages
 - `URL`: The URL your webhook should connect to (only needed for webhook mode)

 - `SUDO_USERS`: A space-separated list of user_ids which should be considered sudo users
 - `SUPPORT_USERS`: A space-separated list of user_ids which should be considered support users (can gban/ungban,
 nothing else)
 - `WHITELIST_USERS`: A space-separated list of user_ids which should be considered whitelisted - they can't be banned.
 - `DONATION_LINK`: Optional: link where you would like to receive donations.
 - `CERT_PATH`: Path to your webhook certificate
 - `PORT`: Port to use for your webhooks
 - `DEL_CMDS`: Whether to delete commands from users which don't have rights to use that command
 - `STRICT_GBAN`: Enforce gbans across new groups as well as old groups. When a gbanned user talks, he will be banned.
 - `WORKERS`: Number of threads to use. 8 is the recommended (and default) amount, but your experience may vary.
 __Note__ that going crazy with more threads wont necessarily speed up your bot, given the large amount of sql data 
 accesses, and the way python asynchronous calls work.
 - `BAN_STICKER`: Which sticker to use when banning people.
 - `ALLOW_EXCL`: Whether to allow using exclamation marks ! for commands as well as /.

  ### Python dependencies

Install the necessary Python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all the necessary python packages.

  ### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I use Postgres, so I recommend using it for optimal compatibility.

In the case of Postgres, this is how you would set up a database on a Debian/ubuntu system. Other distributions may vary.

- install postgresql:

`sudo apt-get update && sudo apt-get install postgresql`

- change to the Postgres user:

`sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

`createuser -P -s -e YOUR_USER`

This will be followed by you need to input your password.

- create a new database table:

`createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever DB you're using (eg Postgres, MySQL, SQLite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and DB name.

  ## Modules
   ### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

   ### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file is in the modules folder.

To add commands, make sure to import the dispatcher via

`from SaitamaRobot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user-friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the DB.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.


## How to setup on Heroku 
For starters click on this button 

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/Pirate-Hunter/One-Piece-Theme-Bot.git) 


## Credits
The bot is based on the original work done by [PaulSonOfLars](https://github.com/PaulSonOfLars) also clone of [SaitamaRobot](https://t.me/SaitamaRobot).
This repo was just revamped to suit an Anime-centric community. All original credits go to Paul and his dedication, Without his efforts, this fork would not have been possible!

Any other authorship/credits can be seen through the commits.

Should any be missing kindly let us know at [One Piece Base](https://t.me/OnePieceBase) or simply submit a pull request on the README.
