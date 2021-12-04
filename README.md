# practice-bot
import telebot
from telebot.types import Message
import requests
from bs4 import BeautifulSoup
from datetime import datetime
import random
from time import sleep

API_KEY = ""#ENTER API KEY HERE
bot = telebot.TeleBot(API_KEY)

@bot.message_handler(commands=["start", "help"])
def starts(message):
    bot.send_message(message.chat.id, "Assalamualaikum "+ message.chat.first_name+", \nWelcome to Hadith Verification bot v1.0.9.3 . In this bot you can verify grade or authenticity of a hadith from the following books:\n\n1) Sahih Bukhari\n2) Sahih Muslim\n3) Sunan Nasai\n4) Sunan Abu Dawood\n5)Sunan Tirmidhi\n6) Sunan Ibn Majah\n7) Musnad Ahmad (only upto Hadith No. 1438)\n8) Al-Adab Al-Mufrad(<=Use this spelling)\n\nType or click on:\n/help to see instructions and query submissions details again.\n/random to see a random hadith.\nat anytime.\n\nWe are working on improving this bot Urdu versions will be available soon Inshallah. Contact @abdulmuizz0903 for any queries or suggestions.\n\nTo get started text the Hadith number with book (like this \"Sahih Bukhari 1035\" write name of book before the hadith number) and this bot will send the full hadith back to you with its Grade(Sahih, Dai'f, Maudu, etc.) IF IT IS NOT FROM SAHIHAIN(Bukhari and Muslim).\nSend your Hadith to get Started. ")
    print("Started By: "+message.chat.first_name)
    id = open("id.txt", "+a")
    id.write("," + str(message.chat.id))
    id.close()
    now = datetime.now()
    current_time = now.strftime("%Y-%m-%d %H:%M:%S")
    if type(message.chat.username) == type(None):
        a = open("log.txt", "+a")
        try:
            a.write("Started by "+message.chat.first_name+", username not available. "+current_time+"\n")
        except:
            a.write("Started by Unknown. Username not available\n")
        a.close()
    else:   
        a = open("log.txt", "+a")
        try:#used exception here because people with first name any other language face error
            a.write("Started by "+message.chat.first_name+", username:"+ message.chat.username+". "+current_time+"\n")
        except:
            a.write("Started by Unknown, username:"+ message.chat.username+". "+current_time+"\n")
        a.close()
@bot.message_handler(commands=["random"])
def randomHadith(message):
    url = f"https://sunnah.com/bukhari:{random.randrange(1, 7563, 1)}"
    content = requests.get(url)
    htmlContent = content.content
    soup = BeautifulSoup(htmlContent, "html.parser")
    bot.send_message(message.chat.id, soup.find("div", class_="hadith_reference_sticky").get_text()+"\n"+soup.find("div", class_="arabic_hadith_full arabic").get_text()+"\n")
    bot.send_message(message.chat.id, soup.find("div", class_="hadith_narrated").get_text() +"\n"+ soup.find("div", class_="text_details").get_text())
    now = datetime.now()
    current_time = now.strftime("%Y-%m-%d %H:%M:%S")
    if type(message.chat.username) == type(None):
        a = open("log.txt", "+a")
        try:#used exception here because people with first name any other language face error
            a.write("Used by "+message.chat.first_name+" username: Not availble. "+current_time+"\n")
        except:
            a.write("Used by Unknown, username: Not availble. "+current_time+"\n")
        a.close()
    else:   
        a = open("log.txt", "+a")
        try:
            a.write("Used by "+message.chat.first_name+", username:"+ message.chat.username+". "+current_time+"\n")
        except:
            a.write("Used by Unknown. username:"+ message.chat.username+". "+current_time+"\n")
        a.close()
    id = open("id.txt", "+a")
    id.write("," + str(message.chat.id))
    id.close()
    
def passin(message):
    return True
@bot.message_handler(func=passin)
def convert1(message):
    try:
        hadith = message.text 
        hadith_list = hadith.split()

        for q in hadith_list:
            if q == "Bukhari" or q == "bukhari":
                for z in hadith_list:
                    for y in z:
                        if y == "0" or "1" or "2" or "3" or "4" or "5" or "6" or "7" or "8" or "9":
                            hadith = z
                            break
                        else:
                            continue
                book = "bukhari"
                break
            elif q == "Muslim" or q == "muslim":
                for z in hadith_list:
                    for y in z:
                        if y == "0" or "1" or "2" or "3" or "4" or "5" or "6" or "7" or "8" or "9":
                            hadith = z
                            break
                        else:
                            continue
                book = "muslim"
                break
            elif q == "Nasai" or q == "nasai":
                for z in hadith_list:
                    for y in z:
                        if y == "0" or "1" or "2" or "3" or "4" or "5" or "6" or "7" or "8" or "9":
                            hadith = z
                            break
                        else:
                            continue
                book = "nasai"
                break
            elif q == "Abu-Dawood" or q == "abu-dawood"  or q == "Abu" or q == "abu" or q == "abi":
                for z in hadith_list:
                    for y in z:
                        if y == "0" or "1" or "2" or "3" or "4" or "5" or "6" or "7" or "8" or "9":
                            hadith = z
                            break
                        else:
                            continue
                book =
