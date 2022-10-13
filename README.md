# PANIC-monitoring-HAQQ-
![2022-10-13_22-42-48](https://user-images.githubusercontent.com/100706570/195697353-db23bc91-11c0-4a0b-8e23-d8b45c996114.png)

 # PANIC monitoring and alerting for HAQQ blockchain

PANIC is an open source monitoring and alerting solution for Cosmos-SDK, Substrate and Chainlink based nodes by Simply VC. The tool was built with user friendliness in mind, and comes with numerous features such as phone calls for critical alerts, a UI Dashboard, a Web-UI installation process and Telegram/Slack commands for increased control over your alerter.

 # Installation Guide
We will now guide you through the steps required to get PANIC up and running. We recommend that PANIC is installed on a Linux system and that everything needed in the Requirements section is done before the installation procedure is started.

Installation
TIP: If your terminal is telling you that you do not have permissions to run a command try adding sudo to your command e.g, sudo docker --version this will run your command as root.

Installing Git
*Skip if Git is already installed.

  ```
  # install git
  sudo apt install git
  
  check
  git --version
  ```
#### Installing Docker and Docker Compose

Skip if Docker and Docker Compose is already installed

```
# install docker and docker-compose
curl -sSL https://get.docker.com/ | sh
sudo apt install docker-compose -y

check
docker --version
docker-compose --version
```
These should give you the current versions of the software that have been installed. At the time of writing the current working docker version is 20.10.10 while the docker-compose version is 1.25.0. If you have a different version that doesn't allow you to run the docker-compose.yml file then either upgrade your versions of docker and docker-compose or change the version inside of the docker-compose.yml file which is currently at 3.7.

Install configuration

```
# clone the repo and go to the
git clone https://github.com/SimplyVC/panic
cd panic
```

In the `panic` directory, edit the parameters in the `.env` file

- INSTALLER_USERNAME: user

- INSTALLER_PASSWORD: password

Once inside change UI_ACCESS_IP, INSTALLER_USERNAME and INSTALLER_PASSWORD accordingly. Here is an example:

```
UI_ACCESS_IP=1.1.1.1
INSTALLER_USERNAME=panic_user
INSTALLER_PASSWORD=panic_password
```
Then to exit hit the following keys:

To exit your .env file: CTRL + X
To select yes to save your modified file: Y
To confirm the file name and exit: ENTER


Launch Panic

After configuring all the parameters run Panic with this command:

``bash
docker-compose up -d --build
```
If the build fails, we remove the docker images with the following command, fix the cause of the failure and start the build again:

```bash
docker-compose kill
docker system prune -a --volumes
docker-compose up -d --build
```

To make sure that the system is working correctly, you can use the commands `docker-compose logs -f alerter` and `docker-compose logs -f health-checker`.

The log files are located in the `panic/alerter/logs` directory

Setting up Telegram notifications

To create **Telegram bot**, add [@BotFather](https://telegram.me/BotFather) to Telegram, click Start, and perform the following steps:

1. send a command `/newbot` and give the requested data including bot name and user name

2. Write down API token, which looks like:`11111111:AAA-AAA11111111-aaaaa11111`.

3. Click on the link `t.me/<username>` to access the created bot and click `Start`.

4. Follow the link `api.telegram.org/bot<token>/getUpdates`, replacing the `<token>` received bot token. Opens up a list of bot activity, including the messages sent to him

5. There should be at least one message in the list, triggered by clicking Start. If not, send the bot the `/start` command. Fix the value of `"id"` in the `"chat"` section.

6. This completes the creation of the bot, to create another bot, repeat the above steps again

   **As a result we should get

   - Telegram account
   - Telegram bot
   - Telegram bot API token
   - Chat ID (`chat ID`) 

Configuring monitoring and alerts

The configuration of node monitoring and notification channels is done at `https://{UI_ACCESS_IP}:8000`. For authorization we use `INSTALLER_USERNAME` and `INSTALLER_PASSWORD` which we specified in file `.env`. 

After authorization, the monitoring wizard starts. All necessary actions are intuitive and commented in detail.
![2022-10-13_22-41-47](https://user-images.githubusercontent.com/100706570/195697381-83d3af22-439c-42ae-bc87-d38de3b58970.png)
