# lab_3-4

## Creating bot

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled.png)

## Creating environment

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%201.png)

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%202.png)

## Receiving from bot

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%203.png)

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%204.png)

## Publish to github

[GitHub - izumisagirii/7940lab3-4](https://github.com/izumisagirii/7940lab3-4)

## Creating redis database

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%205.png)

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%206.png)

## Response with database

add and test new method

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%207.png)

## Using HKBU-GPT api

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%208.png)

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%209.png)

## Publishing on github

[https://github.com/izumisagirii/7940lab3-4](https://github.com/izumisagirii/7940lab3-4)

for security concern, gpt token has not been published.

## Write ups

1. The current chatbot system is built on the Telegram Bot API and uses several components:
    1. **Updater**: This component connects to the Telegram server using the bot’s token, retrieves updates (new messages), and passes them to the Dispatcher.
    2. **Dispatcher**: This component handles updates based on their type. It uses handlers to process command messages (like “/add”, “/help”, “/hello”) and text messages.
    3. **Command Handlers**: These are specific handlers for command messages. Each command has its own handler function (like **`add`**, **`help_command`**, **`hello_command`**) that processes the command and sends a response.
    4. **Message Handler**: This handler processes text messages that are not commands. It uses the **`equiped_chatgpt`** function to generate a response using the HKBU_ChatGPT model.
    5. **Redis**: This is an in-memory data structure store, used as a database in this case. It’s used to count how many times a keyword has been said.
    6. **Logging**: This component logs important events, which can be useful for debugging and understanding the bot’s behavior.
2. The chatbot handles special commands using the **`CommandHandler`** class from the **`telegram.ext`** module. Each command is associated with a specific function that gets executed when the command is issued by a user. 
3. Buy adding these lines to chatbot.py

```python
dispatcher.add_handler(CommandHandler("hello", hello_command))

...

def hello_command(update: Update, context: CallbackContext) -> None:
    """Send a message when the command /hello is issued."""
    try:
        logging.info(context.args[0])
        msg = context.args[0]  # /add keyword <-- this should store the keyword
        update.message.reply_text('Good day ' + msg + '!')
    except (IndexError, ValueError):
        update.message.reply_text('Usage: /add <keyword>')
```

![Untitled](lab_3-4%20eb4f9a63224949a59d8771974e528dbd/Untitled%2010.png)

1. publishing

[https://github.com/izumisagirii/7940lab3-4](https://github.com/izumisagirii/7940lab3-4)