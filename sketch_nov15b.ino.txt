#include <ESP8266WiFi.h>
#include "DHT.h"

#define DHTPIN D4          // DHT sensor pin
#define DHTTYPE DHT11      // DHT11 or DHT22
DHT dht(DHTPIN, DHTTYPE);

const char* ssid = "vivo";        
const char* password = "12345678";   

String apiKey = "F1YBTFI7M62CCZGS";  

const char* server = "api.thingspeak.com";

WiFiClient client;

void setup() {
  Serial.begin(9600);
  dht.begin();
  
  Serial.println("Connecting to WiFi...");
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nWiFi Connected!");
}

void loop() {
  float h = dht.readHumidity();
  float t = dht.readTemperature(); 
  int rainAnalog = analogRead(A0);     

  // Rain percentage calculation
  int rainPercent = map(rainAnalog, 1023, 0, 0, 100);  
  rainPercent = constrain(rainPercent, 0, 100);

  Serial.println("------------------------------");
  Serial.print("Temperature: ");
  Serial.println(t);
  Serial.print("Humidity: ");
  Serial.println(h);
  Serial.print("Rain Level (%): ");
  Serial.println(rainPercent);
  Serial.println("------------------------------");
  
  if (client.connect(server, 80)) {
    String postStr = apiKey;
    postStr += "&field1=";
    postStr += String(t);
    postStr += "&field2=";
    postStr += String(h);
    postStr += "&field3=";
    postStr += String(rainPercent);
    postStr += "\r\n\r\n";

    client.print("POST /update HTTP/1.1\n");
    client.print("Host: api.thingspeak.com\n");
    client.print("Connection: close\n");
    client.print("X-THINGSPEAKAPIKEY: " + apiKey + "\n");
    client.print("Content-Type: application/x-www-form-urlencoded\n");
    client.print("Content-Length: ");
    client.print(postStr.length());
    client.print("\n\n");
    client.print(postStr);

    Serial.println("Data Sent to ThingSpeak!");
  }

  client.stop();
  
  Serial.println("Waiting 15 seconds...");
  delay(15000);   // ThingSpeak minimum delay
}
