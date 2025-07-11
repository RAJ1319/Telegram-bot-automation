# Telegram-bot-automation
import os
import random
import time
import pyautogui
import pyperclip

# Folder paths
meme_folder = os.path.join("telegram_content", "memes")
caption_file = os.path.join("telegram_content", "captions.txt")

# Hashtag sets
hashtags_news = [
    "#FakeNews", "#MediaBias", "#BreakingNews", "#NewsLeak", "#TRPwar",
    "#PressFreedom", "#JournalismMatters", "#NewsVsTruth", "#MediaWatch", "#Disinformation"
]
hashtags_corporate = [
    "#CorporateGreed", "#BigCorporations", "#CorruptCorporates", "#ProfitOverPeople",
    "#CorporateScam", "#BusinessEthics", "#ExposeTheRich", "#EconomicInjustice",
    "#MonopolyAlert", "#CorporateAccountability"
]
hashtags_political = [
    "#PoliticalDrama", "#PowerHungry", "#NetajiExposed", "#VoteForTruth",
    "#ScamPolitics", "#DynastyPolitics", "#PoliticsUnmasked", "#ChunaaviJumla",
    "#PoliticalAgenda", "#PublicVsPolitics"
]

# Load memes & captions
memes = [f for f in os.listdir(meme_folder) if f.endswith((".jpg", ".png"))]
with open(caption_file, "r", encoding="utf-8") as f:
    all_captions = [line.strip() for line in f if line.strip()]

# Select one meme
selected_meme = random.choice(memes)

# Select 2–3 captions
selected_captions = random.sample(all_captions, random.randint(2, 3))

# Select hashtags
selected_hashtags = random.sample(hashtags_news, 2) + \
                    random.sample(hashtags_corporate, 2) + \
                    random.sample(hashtags_political, 2)

# Create final message
final_message = "\n".join(selected_captions) + "\n\n" + " ".join(selected_hashtags)

# Full meme path
meme_path = os.path.abspath(os.path.join(meme_folder, selected_meme))

# Start automation
time.sleep(5)  # Time to switch to Telegram window manually

# Open file dialog and paste meme path
pyperclip.copy(meme_path)
pyautogui.hotkey("ctrl", "o")
time.sleep(1)
pyautogui.hotkey("ctrl", "v")
pyautogui.press("enter")
time.sleep(1)

# Paste caption with hashtags
pyperclip.copy(final_message)
pyautogui.hotkey("ctrl", "v")

# Send
time.sleep(1)
pyautogui.press("enter")
