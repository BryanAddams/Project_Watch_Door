/*
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
*/

#include <ESP8266WiFi.h> // Includes the library to connect the ESP8266 to the WiFi network | Inclui a biblioteca para conectar o ESP8266 à rede WiFi
#include <WiFiClientSecure.h> // Includes the library to create a secure WiFi client | Inclui a biblioteca para criar um cliente WiFi seguro
#include <UniversalTelegramBot.h> // Includes the library to interact with the Telegram bot | Inclui a biblioteca para interagir com o bot do Telegram

#define Pin_Alarm D1 // Defines the alarm pin | Define o pino do alarme
#define PIR_Sensor D0 // Defines the PIR sensor pin | Define o pino do sensor PIR
int Alarm_Time = 5000; // Defines the alarm time in milliseconds | Define o tempo de alarme em milissegundos
int Pause_Time = 60000; // Defines the pause time in milliseconds | Define o tempo de pausa em milissegundos

const char* ssid = "SSID_wifi"; // Defines the WiFi network SSID | Define o SSID da rede WiFi
const char* password = "senha_wifi"; // Defines the WiFi network password | Define a senha da rede WiFi

#define BOTtoken "Token_Bot" // Defines the Telegram bot token | Define o token do bot do Telegram
#define CHAT_ID "Seu_Chat_ID" // Defines the Telegram chat ID | Define o ID do chat do Telegram
WiFiClientSecure client; // Creates a secure WiFi client | Cria um cliente WiFi seguro
UniversalTelegramBot bot(BOTtoken, client); // Creates a Telegram bot | Cria um bot do Telegram

void setup() {
  Serial.begin(9600); // Starts the serial communication at 9600 baud | Inicia a comunicação serial a 9600 baud
  pinMode(PIR_Sensor, INPUT); // Sets the PIR sensor pin as input | Define o pino do sensor PIR como entrada
  pinMode(Pin_Alarm, OUTPUT); // Sets the alarm pin as output | Define o pino do alarme como saída
  digitalWrite(Pin_Alarm, LOW); // Sets the initial state of the alarm pin as low | Define o estado inicial do pino do alarme como baixo

  Serial.print("Connecting to "); // Prints the message on the serial port | Imprime a mensagem na porta serial
  Serial.println(ssid); // Prints the SSID on the serial port | Imprime o SSID na porta serial
  WiFi.begin(ssid, password); // Connects to the WiFi network | Conecta à rede WiFi
  while (WiFi.status() != WL_CONNECTED) { // While the WiFi connection is not established | Enquanto a conexão WiFi não estiver estabelecida
	delay(500); // Waits half a second | Aguarda meio segundo
	Serial.print("."); // Prints a dot on the serial port | Imprime um ponto na porta serial
  }
  Serial.println(""); // Prints an empty line on the serial port | Imprime uma linha vazia na porta serial
  Serial.println("WiFi connected"); // Prints the message on the serial port | Imprime a mensagem na porta serial

  client.setInsecure(); // Sets the client as insecure | Define o cliente como inseguro
}
void loop(){
  bool state = digitalRead(PIR_Sensor); // Reads the state of the PIR sensor | Lê o estado do sensor PIR
  delay(500); // Waits half a second | Aguarda meio segundo
  if(state == HIGH){ // If the state of the PIR sensor is high | Se o estado do sensor PIR for alto
	bot.sendMessage(CHAT_ID, "Movement detected!", ""); // Sends a message to the Telegram chat | Envia uma mensagem para o chat do Telegram
	digitalWrite (Pin_Alarm, HIGH); // Sets the state of the alarm pin as high | Define o estado do pino do alarme como alto
	delay(Alarm_Time); // Waits the alarm time | Aguarda o tempo de alarme
	digitalWrite (Pin_Alarm, LOW); // Sets the state of the alarm pin as low | Define o estado do pino do alarme como baixo
	delay(Pause_Time); // Waits the pause time | Aguarda o tempo de pausa
  }
  else {
	digitalWrite (Pin_Alarm, LOW); // Sets the state of the alarm pin as low | Define o estado do pino do alarme como baixo
  }
}

