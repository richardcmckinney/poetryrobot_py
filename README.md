# Poetry Robot

[Poetry Robot](https://twitter.com/poetryrobot) retweets and encourages Twitter poets. It used to be [a Ruby script](https://github.com/annejohnson/poetryrobot) that ran on an AWS EC2 instance. It's now in Python and runs on AWS Lambda.

## Setup

- Change into the code directory where this is cloned.
- Ensure you're running with Python 3 and a compatible version of pip.
- Run the following to install external dependencies into the code directory:

```
pip install python-twitter -t $(pwd)
```

- Create a `credentials.json` file based on `credentials.example.json`.
- Open a Python interpreter and run:

```python
import poetryrobot
```

- You can now run code like:

```python
poetryrobot.follow_followers()
tweets = poetryrobot.poem_tweets()
poetryrobot.retweet_someone(tweets)
poetryrobot.reply_to_someone(tweets)
```

## Deployment

- Compress the files in the code directory (not including the directory itself) into a zip file.
  - This includes the python-twitter files/directories.
- Upload the zip file into an AWS Lambda function.
- Ensure the Lambda function handler is `poetryrobot.lambda_handler`.
- Ensure the Lambda function has an active trigger (like a CloudWatch scheduled event).
- Ensure the role assigned to the Lambda function allows for writing logs (e.g. `lambda_basic_execution` role).
- Click to test out the lambda function.
  - Activity should occur on Twitter.
  - Log output should be written to CloudWatch.
