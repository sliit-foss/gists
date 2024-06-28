# <center>WhatsApp Bot installation - Multi Device </center>
## Description
This is a WhatsApp bot installation guide for [levanter](https://github.com/lyfe00011/whatsapp-bot-md.git) bot. The bot is unofficial and is not affiliated with WhatsApp. 

## Prerequisites
- A smartphone with an active WhatsApp account.
- A cloud server (VPS) or a local machine (Should be online 24/7).

## Installation
 ### 1. Install with a script
- Run the following command to install the bot.  
```bash
wget -N -O levanter.sh http://bit.ly/43JqREw && chmod +x levanter.sh && ./levanter.sh
```
- Follow the on-screen instructions to complete the installation.
 ### 2. Manual installation
 - Install **git** , **ffmpeg** and **curl**.
 ```bash
    sudo apt update -y && sudo apt upgrade -y
    sudo apt install git ffmpeg curl -y 
```
- Install nodejs.
```bash
sudo apt -y remove nodejs
curl -fsSl https://deb.nodesource.com/setup_lts.x | sudo bash - && sudo apt -y install nodejs
```
- Install yarn.
```bash
npm install -g yarn
```
- Install pm2.
```bash
sudo yarn global add pm2
```
- Clone the repository and install packages.
  > Note: Replace **nameforbot** with the name you want to give to the bot.
```bash
git clone https://github.com/lyfe00011/whatsapp-bot-md nameforbot
cd nameforbot
yarn install --network-concurrency 1
```
- Edit environment variables if needed. Copy and past the lines below to the terminal.
  > Note: Replace only if necessary or remove the line.
  **Session_Id_you_Got_After_Scan_Dont_Add_This_Line_If_You_Can_Scan_From_Terminal_Itself** with the session id you got after scanning the QR code.
   + Go to this [link](https://qr-hazel-alpha.vercel.app/md) to get the session id.
```bash
echo "SESSION_ID = Session_Id_you_Got_After_Scan_Dont_Add_This_Line_If_You_Can_Scan_From_Terminal_Itself
PREFIX = .
STICKER_PACKNAME = LyFE
ALWAYS_ONLINE = false
RMBG_KEY = null
LANGUAG = en
WARN_LIMIT = 3
FORCE_LOGOUT = false
BRAINSHOP = 159501,6pq8dPiYt7PdqHz3
MAX_UPLOAD = 200
REJECT_CALL = false
SUDO = 989876543210
TZ = Asia/Kolkata
VPS = true
AUTO_STATUS_VIEW = true
SEND_READ = true
AJOIN = true
DISABLE_START_MESSAGE = false
PERSONAL_MESSAGE = null" > config.env
``` 

# Edit the config.env file (if needed) and start the bot.
- To edit the config.env file, run the following command.
  > You can find the environment variables documentation [here](https://github.com/lyfe00011/whatsapp-bot-md/wiki/Environment_Variables).
```bash
nano config.env
```
- Start the bot.
```bash
pm2 start . --name botName --attach --time
```
> if that doesn't work, try running `pm2 start index.js --name botName --attach --time` instead. ***botName*** is the name you want to give to the bot. and you must be in the bot directory.
- To stop the bot, run the following command.
```bash
pm2 stop botName
```
- For more pm2 commands, visit the [pm2 documentation](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/).
  
# Usage
* After bot is started, you will receive a text in your whatsapp to your whatsapp number (***self chat***) with the prefix and basic commands.