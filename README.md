Project: Watch Door
Author: Bryan de Sousa Lima

Required libraries:
 ESP8266WiFi.h: This library is required to connect ESP8266 to WiFi network.
 WiFiClientSecure.h: This library is used to create a secure WiFi client.
 UniversalTelegramBot.h: This library allows interaction with the Telegram bot.

How to create a bot and get the token: https://www.siteguarding.com/en/how-to-get-telegram-bot-api-token

How to get your Chat ID:
 - In the Telegram app, search for the bot @username_to_id_bot
 - Send /start
 - At the end of the message it will say your Chat_ID

SSID is just the name of your Wifi
*/

//*****************************************************************************

/* PT-BR

Projeto: Watch Door
Autor: Bryan de Sousa Lima

Bibliotescas necessárias:
    ESP8266WiFi.h: Esta biblioteca é necessária para conectar o ESP8266 à rede WiFi.
    WiFiClientSecure.h: Esta biblioteca é usada para criar um cliente WiFi seguro.
    UniversalTelegramBot.h: Esta biblioteca permite a interação com o bot do Telegram.

Como criar um bot e obter o token: https://www.siteguarding.com/en/how-to-get-telegram-bot-api-token

Como obter seu ID Chat:
   - No app telegram busque pelo bot @username_to_id_bot
   - Envia /start
   - No final da mensagem ele dira seu Chat_ID

SSID é apenas o nome do seu Wifi


COMPONENTS

MB9E Board - A3 - ESP8266 NodeMcu ESP-12 WIFI CH340
PIR Presence Motion Sensor - HC-SR501
Protoboard - 170 holes and 830 holes
Jumpers
Source V5 - USB V8


COMPONENTES

Placa MB9E - A3 - ESP8266 NodeMcu ESP-12 WIFI CH340
Sensor de Movimento Presença PIR - HC-SR501
Protoboard - 170 furos e 830 furos
Jumpers
Fonte V5 - USB V8


//**************************************

Portas/Ports

Buzzer: + D1

Sensor PIR: 
   - VCC: VV
   - OUT: D0
