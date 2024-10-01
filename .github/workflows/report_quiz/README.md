## REPORT QUIZ BOT

[![Build Status](https://github.com/osscameroon/report-quiz/actions/workflows/main.yml/badge.svg)](https://github.com/osscameroon/report-quiz/actions/workflows/main.yml)

## Description

This is an automated workflow for the report quiz bot. This quiz bot performs the following actions

- Selects a random quiz from https://quizapi.io/api/ website
- It periodically sends a message in the group to start a quiz competition
- It stores the results of each quiz inside of a json file located **archive** folder
- Once the quiz is over, it sends a message in the group with the results

### How to run this locally

1. Clone the repository

2. Locate the .github/workflows/report-quiz folder in the root of the repository

3. Run the following command to make a copy of the env.example.sh file

   ```bash
   cp env.example.sh env.sh
   ```

4. Edit the env.sh file with the necessary data

   - Edit the **TELEGRAM_BOT_TOKEN** variable
      - **How to get a telegram BOT Token**
         - Visit https://telegram.me/BotFather
         - Use the command **/newbot** and follow the instructions to create a new bot
         - Copy the token from @BotFather telegram bot and paste the token in the env.sh file

   - Edit the **TELEGRAM_GROUP_ID** variable
      - **How to get a telegram Group ID**
        - You remember the bot you just created? Now take that bot and add it into any group of your choice [How to add a bot to a telegram group](https://stackoverflow.com/questions/37338101/how-to-add-a-bot-to-a-telegram-group)
        - Now visit this site `https://api.telegram.org/bot[BOT_TOKEN_HERE]/getMe`
        - replace `[BOT_TOKEN_HERE]` with the bot token you got from bot BotFather
        - When the page opens ensure you can see a page looking like this
        - ![image](https://github.com/user-attachments/assets/9dadba18-154a-479c-a870-adaf63469fa4)
        - Now go to the group you just added the bot and use this command `/start@THE_USERNAME_OF_YOUR_BOT`
        - Replace `THE_USERNAME_OF_YOUR_BOT` with your bots username
        - Now open this link `https://api.telegram.org/bot[BOT_TOKEN_HERE]/getUpdates` and you should see a json object called results. Look for any key with the name **chat** and under it's child elements you will see **id**. Copy the **id** including the `-`(minus) sign in front of the id
        - ![image](https://github.com/user-attachments/assets/610217af-2ed8-4309-a59d-2eea5399ed99)

        - Copy the group ID from the page you just opened and paste it in the env.sh file

   - Edit the **QUIZAPI_KEY** variable
      - **How to get a quizapi key**
        - Visit https://quizapi.io/
        - Create an account
        - Visit https://quizapi.io/api/ page and generate a new key. Copy the key and paste it in the env.sh file

5. Setting up your bash terminal to run the bot

   - Run the following command in your terminal. Ensure that you have `jq` and `git` installed, if not install them using `sudo apt install jq git`


   ```bash
   source main.sh
   chmod +x main.sh
   ```


   - Now to run this bot, you need to run the commands in a following order for them to work normally. All the functions are located in `.github/workflows/report_quiz/quiz/functions.sh` file


   ```bash
   . main.sh; start_quiz_competition # Use this command to send/initiate a quiz competition in the group
   . main.sh; fetch_quiz_users_answers # Use this command to fetch the users answers before stoping the quiz
   . main.sh; stop_quiz_competition # Use this command to stop the quiz and to prepare for sending results
   ```


6. Please, feel free to contribute to make this bot better. Thanks
