# X Bot on Heroku: Getting Started Guide

This README will walk you through the process of setting up a Twitter (X) bot on Heroku. The bot can be used for a wide range of purposes, from automating posts and replies to interacting with users and gathering insights. This guide will cover everything you need to know, including obtaining API credentials, setting up accounts, and deploying your bot on Heroku.

---

## 🚀 Project Overview

This bot is designed to automate interactions on X (formerly Twitter) using the **Twitter API v2**. You can use this bot to:
- Post tweets automatically on a schedule.
- Respond to tweets or mentions.
- Like, retweet, or follow accounts based on specific keywords or criteria.
- Generate AI-powered content or replies using tools like GPT.
- Analyze user engagement and track trending hashtags.

This project leverages Python, the Tweepy library, and Heroku for seamless deployment and scaling.

---

## 🔧 Prerequisites

Before you begin, make sure you have the following:
1. **Twitter Developer Account** - To access Twitter's API.
2. **API Keys and Tokens** - For authenticating requests to Twitter.
3. **Heroku Account** - To deploy the bot.
4. **Git** - For version control.
5. **Python 3.x** - For running the bot locally before deployment.

### 1. Creating a Twitter Developer Account
- Go to the [Twitter Developer Portal](https://developer.twitter.com/) and sign in with your Twitter account.
- Create a new project and app. This will give you access to the necessary **API keys and tokens**.
- Ensure your app has **Elevated Access** to use endpoints like posting tweets, reading mentions, and more.

### 2. Obtaining API Credentials
You'll need the following credentials:
- **API Key**
- **API Secret Key**
- **Bearer Token**
- **Access Token**
- **Access Token Secret**

Once you have these, create a `.env` file to store them securely:

```
TWITTER_API_KEY=your_api_key
TWITTER_API_SECRET=your_api_secret
TWITTER_ACCESS_TOKEN=your_access_token
TWITTER_ACCESS_TOKEN_SECRET=your_access_token_secret
```

### 3. Creating a Heroku Account
- Sign up for a free account on [Heroku](https://www.heroku.com/).
- Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) on your system.

---

## 🛠️ Local Setup

### 1. Clone the Repository
First, clone the GitHub repository for your Twitter bot:

```bash
git clone https://github.com/yourusername/twitter-bot.git
cd twitter-bot
```

### 2. Install Dependencies
Make sure you have Python installed, then run:

```bash
pip install -r requirements.txt
```

Dependencies include:
- `tweepy` - For interacting with the Twitter API.
- `schedule` - For scheduling automated tweets.
- `dotenv` - For managing environment variables.

### 3. Running the Bot Locally
Before deploying, test your bot locally:

```bash
python bot.py
```

This should authenticate with Twitter and start performing actions (e.g., posting tweets, liking posts).

---

## 🚀 Deploying to Heroku

### 1. Login to Heroku
```bash
heroku login
```

### 2. Create a New Heroku App
```bash
heroku create your-bot-name
```

### 3. Add Environment Variables to Heroku
```bash
heroku config:set TWITTER_API_KEY=your_api_key
heroku config:set TWITTER_API_SECRET=your_api_secret
heroku config:set TWITTER_ACCESS_TOKEN=your_access_token
heroku config:set TWITTER_ACCESS_TOKEN_SECRET=your_access_token_secret
```

### 4. Deploy the Bot to Heroku
```bash
git add .
git commit -m "Initial commit"
git push heroku main
```

### 5. Scale the Worker
```bash
heroku ps:scale worker=1
```

### 6. Monitor Logs
To check if your bot is running smoothly:

```bash
heroku logs --tail
```

---

## ✨ Customizing the Bot

### Configuring Scheduled Posts
You can schedule tweets by modifying the `schedule` section in `bot.py`:

```python
import schedule

def tweet_something():
    api.update_status("Hello World! This is an automated tweet.")
    
schedule.every().day.at("09:00").do(tweet_something)
```

### Responding to Mentions
To automatically respond to mentions:

```python
mentions = api.mentions_timeline(count=10)
for mention in mentions:
    if "#help" in mention.text.lower():
        api.update_status(f"@{mention.user.screen_name} How can I assist you?", in_reply_to_status_id=mention.id)
```

### Using GPT to Generate Tweets
If you want your bot to generate AI-powered responses:
- Obtain an API key from [OpenAI](https://platform.openai.com/).
- Integrate it with the bot using the `openai` Python library.

---

## 📊 Monitoring & Analytics

Use additional Heroku add-ons like:
- **Papertrail**: For logging.
- **Scheduler**: For running periodic jobs.
- **New Relic**: For performance monitoring.

---

## 🔒 Security Considerations

- **Do not hardcode API credentials** in your code; use environment variables.
- Rotate your API keys periodically to prevent misuse.
- Use the **Heroku Config Vars** section to store sensitive information.

---

## 🛠️ Troubleshooting

- **Bot not posting?** Double-check your API credentials and Twitter app permissions.
- **Heroku deployment issues?** Run `heroku logs --tail` to see detailed error logs.
- **Rate limit errors?** Twitter imposes rate limits on API usage. Make sure your bot complies with the limits to avoid being banned.


Happy Tweeting! 🎉
