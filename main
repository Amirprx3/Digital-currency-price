import telebot
import requests
from datetime import datetime

TOKEN = "TOKEN"
bot = telebot.TeleBot(TOKEN)
URL = "https://api.binance.com/api/v3/ticker/price?symbol=btcusdt"
TIME = datetime.now()

@bot.message_handler(commands=['start', 'help'])
def send_welcome(message):
    if message.text == "/start":
        bot.reply_to(message, "Hello, What currency price do you want? \n\nIf you don't know how to get the price, use this command: /help")
    else:
        bot.reply_to(message, "To get the price of the currency, use USDT at the end of the currency name. example: btcusdt")



@bot.message_handler(func=lambda m: True)
def show_price(message):
    symbol = message.text.upper()
    response = requests.get(f"https://api.binance.com/api/v3/ticker/price?symbol={symbol}")
    
    if response.status_code == 200:
        data = response.json()
        bot.reply_to(message, f"✔️Name : {data['symbol']} \n✔️Price: {data['price']} \n✔️Date: {TIME.date()} \n✔️Time: {TIME.strftime('%X')}")
    else:
        bot.reply_to(message, f"❌({message.text}) notfound!")

bot.infinity_polling()
