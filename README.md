from pyrogram import client, filters
from pyrogram.types import Message

API_ID = "7980695807"
API_HASH = "AAEeXH2vhpMkF6W3hwK72b0iBDKxy18qzHw"  
SESSION_STRING= "Alexa_12_Bot"
YOUTUBE_API_KEY = "AIzaSyD1b2k3Z4a5b6c7d8e9f0g1h2i3j4k5l6m"
app = client(SESSION_STRING, api_id=API_ID, api_hash=API_HASH,session_string=SESSION_STRING, youtube_api_key=YOUTUBE_API_KEY)

@app.on_message(filters.command("start") & filters.private)
def start(client, message: text,
            text="Hello! I am Alexa, your personal assistant. How can I help you today?"):
    message.reply_text("Bot started. Use in a group with a voice chat.")

app.on_message(filters.command("join") & filters.group)
def join_handler(client, message: Message):
    if message.chat.type == "supergroup":
        if message.reply_to_message and message.reply_to_message.voice_chat:
            voice_chat = message.reply_to_message.voice_chat
            if voice_chat.status == "active":
                client.join_voice_chat(message.chat.id, voice_chat.id)
                message.reply_text("Joined the voice chat successfully!")
            else:
                message.reply_text("The voice chat is not active.")
        else:
            message.reply_text("Please reply to an active voice chat to join.")
    else:
        message.reply_text("This command can only be used in supergroups.")
        @app.on_message(filters.command("play") & filters.group)
def play_handler(client, message: Message):
    if message.chat.type == "supergroup":
        if message.reply_to_message and message.reply_to_message.voice_chat:
            voice_chat = message.reply_to_message.voice_chat
            if voice_chat.status == "active":
                # Here you would add the logic to play audio in the voice chat
                message.reply_text("Playing audio in the voice chat!")
            else:
                message.reply_text("The voice chat is not active.")
        else:
            message.reply_text("Please reply to an active voice chat to play audio.")
    else:
        message.reply_text("This command can only be used in supergroups.")

        @app.on_message(filters.command("resume")& filters.group)
        def resume_handler(client, message: Message):
            if message.chat.type == "supergroup":
                if message.reply_to_message and message.reply_to_message.voice_chat:
                    voice_chat = message.reply_to_message.voice_chat
                    if voice_chat.status == "active":
                        # Here you would add the logic to resume audio in the voice chat
                        message.reply_text("Resuming audio in the voice chat!")
                    else:
                        message.reply_text("The voice chat is not active.")
                else:
                    message.reply_text("Please reply to an active voice chat to resume audio.")

app.run()                    
