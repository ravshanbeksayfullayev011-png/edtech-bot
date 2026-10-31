import asyncio
import logging
from aiogram import Bot, Dispatcher, types
from aiogram.filters import Command
import google.generativeai as genai

# Tokeningiz va Gemini kalitingiz
TELEGRAM_BOT_TOKEN = "9292464356:AAFjaFt7L6u5gW5VHhL9Q6DkG1TCmRMkLg4"
GEMINI_API_KEY = "AQ.Ab8RN6Lz-F0q4b49lQFgkBLnf2wg_UDwXQWy9ngT3794yyn08w"

# Gemini'ni sozlash
genai.configure(api_key=GEMINI_API_KEY)
model = genai.GenerativeModel("gemini-pro")

# Bot va dispetcherni yaratish
bot = Bot(token=TELEGRAM_BOT_TOKEN)
dp = Dispatcher()

# /start buyrug'i uchun handler
@dp.message(Command("start"))
async def cmd_start(message: types.Message):
    await message.answer("Assalomu alaykum! Men EdTech botman. Menga savol yuborishingiz mumkin.")

# Har qanday matnli xabarga javob berish uchun handler
@dp.message()
async def handle_message(message: types.Message):
    user_text = message.text
    try:
        # Gemini AI'dan javob olish
        response = model.generate_content(user_text)
        await message.answer(response.text)
    except Exception as e:
        await message.answer("Xatolik yuz berdi, iltimos keyinroq urinib ko'ring.")

# Botni ishga tushirish
async def main():
    logging.basicConfig(level=logging.INFO)
    await dp.start_polling(bot)

if __name__ == "__main__":
    asyncio.run(main())
