# Shotbef-llmaschine
Maschine with hx711, ds18b20 and water pump 

/* Wer: hiju1016
 *  Wann: WS 19-20
 *  Was: Shotbefüllmaschine, die über einen Kipphebel bedient wird. Auf dem OLED werden Wassertemperatur und Füllstand des Alkohols angezeigt. */
#include <Adafruit_SSD1306.h>                              // Bibliothek für OLED Bildschirm
#include <Adafruit_GFX.h>                                  // Bibliothek für OLED Bildschirm
#include <Q2HX711.h>                                       // Bibliothek für HX711 Gewichtsensor
#include <OneWire.h>                                       // Bibliothek für DSB18B20 Eindraht-Bus
#include <DallasTemperature.h>                            // Biblothek für DSB18B20
/*******************************************************/
const byte hx711_data_pin = 23;                         // Pinbelegung
const byte hx711_clock_pin = 19;

int zero;                                              // Gobale Variablen definieren
int weight;
void anzeige();
/************************************************************************************/
Q2HX711 hx711(hx711_data_pin, hx711_clock_pin);

#define SCREEN_WIDTH 128                             // OLED initialisieren
#define SCREEN_HEIGHT 64 
#define OLED_RESET 4
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

#define ONE_WIRE_BUS 25                           // GPIO 25 DSB18B20 initialisieren
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);
/****************************************************************************/

void setup()                                             // Setup-Funktion für OLED Display
{
  Serial.begin(115200);
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
  display.display();
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(WHITE);
  zero = (hx711.read()/100);
  sensors.begin();
  delay(2000);
}
/****************************************************************************/
void loop()              
{
  weight = (((hx711.read()/100) - zero)/2)-320;
  sensors.requestTemperatures();
  anzeige();
  delay(2000);
}
/*************************************************************************************************/
void anzeige()                               // Funktion für die Anzeige auf dem OLED I2C Bildschirm
{
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(WHITE);
  display.setCursor(20,5);
  display.println(" Fuellstand: ");
  display.setCursor(25,20);
  display.println(weight);
  display.setCursor(60,20);
  display.println(" ml ");
  display.setCursor(20,35);
  display.println(" Shottemperatur: ");
  display.setCursor(25,50);
  display.println(sensors.getTempCByIndex(0));
  display.setCursor(60,50);
  display.println(" C ");
  display.display();
  delay(1000);
}
/***********************************************************************************************/
  
