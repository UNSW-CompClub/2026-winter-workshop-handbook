# How To Use Your Chatbot Post-Workshop

Hey guys, we're so glad you were able to come to the workshop! It was awesome to see all your chatbots and how each of you put your own spin on them!

Now that you've got your code from the workshop, you'll have to create and set up your own Claude API key to keep using it!

---

## What's an API key?
An API key is like a password that allows you to access Claude's servers. You'll remember that we don't actually use the Claude website to talk to Claude; rather, we connect to Claude's servers (with an API key are our password) and make requests in order to talk to Claude!

---

## Step 1: Create your own API key
The first step involves creating your own key. Unfortunately this step isn't free, and you'll need to pay to access Claude. I'd recommend adding $5-$10 to your account, which gives you access to 1-2 million tokens using Claude Haiku (the model we used during the workshop). Here's the [link](https://platform.claude.com/docs/en/home) (make sure you press Get API Key)

> [!WARNING] Parental Consent
> Make sure to get your parent's approval before buying ANY tokens!

> [!TIP] Other Claude Models
> If you want, you can also experiment with more powerful models from Claude. Just make sure you follow their [platform docs](https://platform.claude.com/docs/en/home). DO NOTE THAT THESE ARE MUCH MORE EXPENSIVE (YOU'LL RUN OUT OF MONEY QUICKER)!!
> E.g., if you switch from Haiku to Fable, you'll only get 100,000 tokens instead of 1,000,000 from $5 of credit, so spend wisely!

> [!WARNING] Parental Consent
> Make sure to get your parent's approval before buying ANY tokens!
> (Yes I put this here twice)

Now that you've got an account and put some credit into it, generate an API key. Make sure to give it a secret you'll remember. Hold on to this, we'll need it.

## Step 2: Adding your API key to your device
Once you've acquired your API key, all you have to do is go into the `.env` file in your codebase, and add your API key here!
```
API_KEY = "your-key-goes-here"
```

Then, test your code and make sure it's all good! You should now be able to use your chatbot as you did during the workshop, and keep playing around with it!

> [!WARNING] GitHub users
> If you're using Git to store your code, remember to add `.env` to your `.gitignore` file, otherwise someone might use your API key!

> [!WARNING] Parental Consent
> Make sure to get your parent's approval before buying ANY tokens!
> (I cannot emphasise this enough y'all)
