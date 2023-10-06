#AddMember-Telegram is a Python 3 script that allows you to migrate members from one Telegram group (Group A) to another (Group B). This can be especially useful when you need to consolidate members from multiple groups into a single supergroup. Please ensure you have the necessary prerequisites and follow the guidelines below to use this script effectively.



Prerequisites
To use this script, you will need the following:

Python 3 environment (compatible with Linux and Windows)
Approximately 20 Telegram accounts to run the script (accounts switch automatically when blocked)
Each account should be a member of both the source and target groups
Take note of your region's phone number format
Your group must be a supergroup. If it's not already, follow the instructions here to convert it.


https://www.wikihow.com/Convert-a-Telegram-Group-to-a-Supergroup-on-PC-or-Mac

Usage

Step 1: Install the telethon package
Install the telethon package using pip:

pip install telethon

Step 2: Create a configuration file (config.json)

* Step 2: Create file config.json

Copy the config.example.json file and create a config.json file. Update the following fields:


{
	"group_target": 1398120166, // Target group ID
	"group_source": 1490302444, // Source group ID
	"accounts": [ // Array of Telegram accounts
		{
			"phone": "+84XXXX", // Your phone number
			"api_id": 1234566, // API ID from https://my.telegram.org/apps
			"api_hash": "57c6f3c72c2f21676d53be2eXXXXXX" // API hash from https://my.telegram.org/apps
		}
	]
}


group_target and group_source: After running get_data.py, check the files in the data/group directory.

accounts: List your Telegram accounts. For each account/phone number, create an app at https://my.telegram.org/apps and copy the api_id and api_hash into the config file.

Step 3: Initialize sessions

Run the following command to initialize sessions for your accounts:

python init_session.py


* Step 4: run `python get_data.py` to get data of group, data user and save file in folder `data`

![Get data](images/step2.png)
![Data after Get](images/data_step2.png)

```
{
    "user_id": "847587728",
    "access_hash": "2393668282771176567",
    "username": "None"
}
```
One group have one list user (list username), but each account Telegram have list User (difference user_id, access_hash). Use `user_id` and `access_hash` to add member, so you need get list user of each account Telegram.
Note: Use username have also use to add member, but something use not have username

After run get data, check again file in data/group and edit file config to change group_target, group_source, which you want to add.

* Step 5: run `python add_member.py` to add member from `group_source` to `group_target`
Logic: 
	* after adding 1 member, sleep 2 minutes
	* after each account adds 35 members --> sleep 15 minutes
	* Remove account when there is a Flood Wait Error
	* Break if there are no more accounts

Note: If your account gets blocked, go to https://web.telegram.org/#/im?p=@SpamBot and chat /start to see the time the ban would be lifted

![Get data](images/block.png)

Done!



Create a new issue if you have legit issues and we will do our best to resolve them.

## Contributing:
* Fork the repo on Github
* Clone the repo using `git clone addmember-telegram`
* Make changes and stage the files: `git add .`
* Commit the changes: `git commit -m "Changed a few things"`
* Push the changes to your Github repo: `git push -u origin main`
* Submit a pull request.
