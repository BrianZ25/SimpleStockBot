import requests
from bs4 import BeautifulSoup
import os
import discord

client = discord.Client();

@client.event 
async def on_ready():
  print("Hello, I'm {0.user}".format(client))

@client.event
async def on_message(message):

  if message.content.startswith("!price"):
    Stock_Name = message.content.split("!price ", 1)[1]
    url = "https://finance.yahoo.com/quote/" + Stock_Name
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    price = soup.find("span", {"class": "Trsdu(0.3s) Fw(b) Fz(36px) Mb(-4px) D(ib)"}).text
    await message.channel.send("The price of " + Stock_Name+ " is currently " + price)

  if message.content.startswith("!percentage"):
    Stock_Name = message.content.split("!percentage ", 1)[1]
    url = "https://finance.yahoo.com/quote/" + Stock_Name
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    try:
      percentage = soup.find("span", {"class": "Trsdu(0.3s) Fw(500) Pstart(10px) Fz(24px) C($positiveColor)"}).text
      await message.channel.send("The change of " + Stock_Name + " is " +percentage)
    except:
      percentage = soup.find("span", {"class": "Trsdu(0.3s) Fw(500) Pstart(10px) Fz(24px) C($negativeColor)"}).text
      await message.channel.send("The change of " + Stock_Name + " is " +percentage)
  
  if message.content.startswith("!range"):
    Stock_Name = message.content.split("!range ", 1)[1]
    url = "https://finance.yahoo.com/quote/" + Stock_Name
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    ranges = soup.find("td", {"data-test":"DAYS_RANGE-value"}).text
    await message.channel.send(Stock_Name+ " ranged from "+ranges)

  if message.content.startswith("!open"):
    Stock_Name = message.content.split("!open ", 1)[1]
    url = "https://finance.yahoo.com/quote/" + Stock_Name
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    Open_Price = soup.find("span", {"data-reactid":"97"}).text
    await message.channel.send(Stock_Name+ " opened at "+ Open_Price)

  if message.content.startswith("!graph"):
    Stock_Name = message.content.split("!graph ", 1)[1]
    url = "https://finance.yahoo.com/quote/" + Stock_Name
    url2 = "https://finance.yahoo.com"
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    graph = soup.find("a", {"class":"C($linkColor) Z(1) Fz(s) Fw(500) Ta(end) Pos(a) End(0)"}).get("href")
    await message.channel.send(url2 + graph)

my_secret = os.environ['Key']
client.run(my_secret)

"""
if not using repl.it, use
client.run(Your Discord Token)

instead of 
my_secret = os.environ['Key']
client.run(my_secret)
"""
