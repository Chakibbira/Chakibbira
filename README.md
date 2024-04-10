import requests
import json

# استبدل هذه القيم بقيم حسابك
username = "your_username"
password = "your_password"

# حدد رقم اللعبة
game_id = 12345

# حدد نوع الرهان
bet_type = "thimbles"

# حدد قيمة الرهان
stake = 100

# قم بتسجيل الدخول
session = requests.Session()
login_url = "https://linebet.com/api/v2/auth/login"
login_data = {"username": username, "password": password}
login_response = session.post(login_url, data=login_data)

# تأكد من تسجيل الدخول بنجاح
if login_response.status_code == 200:
    # احصل على معلومات اللعبة
    game_info_url = f"https://linebet.com/api/v2/games/{game_id}/info"
    game_info_response = session.get(game_info_url)
    game_info = json.loads(game_info_response.text)

    # حدد كرة thimbles
    thimble_number = 1 # حدد رقم الكرة هنا

    # قم بوضع الرهان
    bet_url = "https://linebet.com/api/v2/bets/place"
    bet_data = {
        "game_id": game_id,
        "bet_type": bet_type,
        "stake": stake,
        "thimble_number": thimble_number,
    }
    bet_response = session.post(bet_url, data=bet_data)

    # تأكد من وضع الرهان بنجاح
    if bet_response.status_code == 200:
        print("تم وضع الرهان بنجاح!")
    else:
        print("خطأ في وضع الرهان:", bet_response.text)
else:
    print("خطأ في تسجيل الدخول:", login_response.text)
    
