# mortento1
import discord
import random

intents = discord.Intents.default()
intents.message_content = True

client = discord.Client(intents=intents)

list1 = [":wave:", ":triumph:", ":rage:", ":japanese_ogre:", ":skull_crossbones:", ":clown:", ":mechanical_arm:", ":muscle:", ":cold_face:", ":soccer:"]
# Переменная intents - хранит привилегии бота
intents = discord.Intents.default()
# Включаем привелегию на чтение сообщений
intents.message_content = True
# Создаем бота в переменной client и передаем все привелегии
client = discord.Client(intents=intents)

@client.event
async def on_ready():
    print(f'We have logged in as {client.user}')

def gen_pass(pass_length):
    elements = "+-/*!&$#?=@<>QWERTYUIOPASDFGHJKLZXCVBNMqwertyuiopasdfghjklzxcvbnm"
    password = ""
    for i in range(pass_length):
       password += random.choice(elements)

    return password

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$hello'):
        await message.channel.send(f'Привет! Я бот {client.user}!')
    elif message.content.startswith('$bye'):
        await message.channel.send(":wave: :wave: :wave:")
    elif message.content.startswith('$random'):
        await message.channel.send(random.choice(list1))
    elif message.content.startswith('$password'): 
         await message.channel.send(gen_pass(10))
    elif message.content.startswith('$heh'):
        if len(message.content) > 4:
            count_heh = int(message.content[4:])
        else:
            count_heh = 5
        await message.channel.send("he" * count_heh)
    elif message.content.startswith('$angry?'):
        await message.channel.send(":triumph: :rage: :japanese_ogre: :rage: :triumph:")
    else:
        await message.channel.send(message.content)


    



TOKEN = "your token"
client.run(TOKEN)
