# -*- coding: utf-8 -*-
# بوت تيليجرام بسيط:
# - /start أو أي رسالة → يرسل رقم الـ ID مع نص تحته

from telegram import Update
from telegram.ext import (
    ApplicationBuilder,
    CommandHandler,
    MessageHandler,
    ContextTypes,
    filters,
)


async def send_id(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id

    text = f"""🔢 رقم الـ ID الخاص بك:

{user_id}

انسخ رقم الـ ID الخاص بك وضعه في الموقع لتلقي الإشعارات.
"""

    await update.message.reply_text(text, parse_mode="Markdown")


def main():
    # ضع توكن البوت هنا بين علامتي التنصيص
    BOT_TOKEN = ""

    app = ApplicationBuilder().token(BOT_TOKEN).build()

    # أمر /start
    app.add_handler(CommandHandler("start", send_id))

    # أي رسالة نصية (بدون أوامر)
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, send_id))

    print("✅ البوت يعمل الآن...")
    app.run_polling()


if name == "main":
    main()
