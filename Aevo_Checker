import requests

api_key = input("Your API_Key: ")
api_secret = input("Your API_Secret: ")

limit = 1000

url = "https://api.aevo.xyz/account"
headers = {
    "accept": "application/json",
    "AEVO-KEY": api_key,
    "AEVO-SECRET": api_secret,
}
response = requests.get(url, headers=headers)
account_data = response.json()

account = account_data['account']
username = account_data['username']
balance = float(account_data['balance'])
print()
print("Account:", account)
print("Username:", username)
print("Balance:", f"${balance:.4f}")

url_trade_history = "https://api.aevo.xyz/trade-history"
start_time = 0

total_volume_usd = 0
while True:
    params_trade_history = {
        "start_time": start_time,
        "limit": limit,
    }
    headers_trade_history = {
        "accept": "application/json",
        "AEVO-KEY": api_key,
        "AEVO-SECRET": api_secret
    }
    response_trade_history = requests.get(url_trade_history, params=params_trade_history, headers=headers_trade_history)
    trade_history_data = response_trade_history.json()
    
    trades = trade_history_data.get('trade_history', [])
    if not trades:
        break  
    last_trade_time = int(trades[-1]['created_timestamp'])
    for trade in trades:
        if 'price' in trade and 'amount' in trade:
            total_volume_usd += float(trade['amount']) * float(trade['price'])
    start_time = last_trade_time + 1

print(f"Total Trading Volume: ${total_volume_usd:.2f}")
