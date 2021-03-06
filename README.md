<div align="center">

# End A Conference Call With A Text Message

<a href="http://dev.bandwidth.com"><img src="https://s3.amazonaws.com/bwdemos/BW-Voice-Messaging.png"/></a>
</div>

Ever had a conference call where you wanted to end the conference with a text message recap of the meeting? This project shows how you can do that using Bandwidth's Voice and Messaging APIs!

## Table of Contents

* [Prereqs](#prereqs)
* [How It Works](#how-it-works)

## Prereqs

* Bandwidth Application Account (https://app.bandwidth.com)
* A server to run the application, or a tunneling service like ngrok

## How It Works

This project launches a server that creates a conference call after you text a list of phone numbers to you Bandwidth phone number. You can end the conference call by sending a text message to the same Bandwidth phone number, and the contents of that message will be sent to all members of the conference.

Before running the project, the following environmental variables need to be set:

```
BANDWIDTH_USER_ID
BANDWIDTH_API_TOKEN
BANDWIDTH_API_SECRET
BANDWIDTH_PHONE_NUMBER
USER_PHONE_NUMBER
```

BANDWIDTH_USER_ID, BANDWIDTH_API_TOKEN, and BANDWIDTH_API_SECRET can be found on your account on https://app.bandwidth.com.

BANDWIDTH_PHONE_NUMBER is your Bandwidth phone number that will be used for this application.

USER_PHONE_NUMBER is your personal phone number used to start and stop the conference call.

Phone numbers must be in +1XXXYYYZZZZ format.

The python version used in this project is 3.7.0.

Required dependencies can be installed by running the following command:

```
pip install -r requirements.txt
```

To start the server, run the following command

```
python conference_call.py
```

### Setting up the Bandwidth application
Login to https://app.bandwidth.com and create a Bandwidth Application. This application will be both a voice and messaging application. Assign your BANDWIDTH_PHONE_NUMBER to this application.

Make the `Voice callback URL` point to `<your-server>/voice` and the `Messaging callback URL` point to `<your-server>/message`

### Starting the conference
After the server has started, you can text your BANDWIDTH_PHONE_NUMBER from your USER_PHONE_NUMBER a list of numbers to start a conference.

Example text message:

```
+1XXXYYYZZZZ +1AAABBBCCCC +1DDDEEEFFFF
```

Note that your USER_PHONE_NUMBER needs to also be included if you want to be included in the conference call.

Bandwidth's conference calls are limited to 20 participants, so you can send up to 20 numbers.

Each of the numbers you requested to join the conference will receive the following text message:

```
You have been invited by USER_PHONE_NUMBER to join a conference call on BANDWIDTH_PHONE_NUMBER. Please call this number to join.
```

After calling the BANDWIDTH_PHONE_NUMBER, the member will join the conference

You will receive the following text message confirming that you've started the conference:

```
You have started the conference! Please respond to this message when you are ready to end the conference. Your message will be forwarded to all conference participants.
```

### Ending the conference
The next text message sent by your USER_PHONE_NUMBER to your BANDWIDTH_PHONE_NUMBER will signal the end of the conference. You can send anything you like, and that text message will be forwarded to all members of the conference. The conference will then end.
