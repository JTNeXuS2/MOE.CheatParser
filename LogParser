import asyncio
import os
# Need "pip install requests"
import requests
import time
import re

#Set discord webhook URL
webhook_url = "https://discord.com/api/webhooks/1214978965471756418/Ln6OXfl44444444444rrrrrrrrrtttttttttttt"

#Set admins SteamIDs
id_list = ['PostLogin Account: 76561191111111111', 'PostLogin Account: 76561192222222222', 'ServerCheat_Implementation']

#Set full path to logs
log_files = [
    'C:/moe_cluster/MOE/Saved/Logs/SceneServer_1000.log',
    'C:/moe_cluster/MOE/Saved/Logs/SceneServer_2000.log',
    'C:/moe_cluster/MOE/Saved/Logs/SceneServer_3000.log'
]

#Set match the server name and log file
log_files_dict = {
    'SceneServer_1000.log': 'Кластер: PVE1',
    'SceneServer_2000.log': 'Кластер: PVP',
    'SceneServer_3000.log': 'Кластер: PVE2'
}
#Nothing change more

async def read_log_file(file_path):
    try:
        with open(file_path, 'r', encoding='utf-8') as file:
            return file.readlines()
    except FileNotFoundError:
        #print(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] File not found: {file_path}")
        return []

async def send_discord_webhook(webhook_url, message):
    data = {'content': message}
    try:
        requests.post(webhook_url, json=data)
    except Exception as e:
        print(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] Error sending Discord webhook: {e}")

last_lines = {os.path.basename(log_file): None for log_file in log_files}

async def process_log_file(log_file):
    log_lines = await read_log_file(log_file)
    log_filename = os.path.basename(log_file)
    
    if log_filename in last_lines:
        if last_lines[log_filename] is not None:
            new_lines = log_lines[last_lines[log_filename] or 0:]
            for line in new_lines:
                if any(id in line for id in id_list):
                    if re.match(r'\[\d{4}\.\d{2}\.\d{2}-\d{2}\.\d{2}\.\d{2}:\d{1,}\]\[\d{1,}\](LogSG|LogSGGM):', line):
                        server_name = log_files_dict.get(log_filename, "Unknown Server")
                        print(f"{server_name} ({log_filename}): {line}")
                        await send_discord_webhook(webhook_url, f"{server_name} ```({log_filename}): {line}```")
        last_lines[log_filename] = len(log_lines)
    else:
        print(f"Key '{log_filename}' not found in last_lines dictionary")


async def main():
    while True:
        tasks = [process_log_file(log_file) for log_file in log_files]
        await asyncio.gather(*tasks)
        await asyncio.sleep(10)  # Проверка каждые 10 секунд

if __name__ == '__main__':
    asyncio.run(main())
