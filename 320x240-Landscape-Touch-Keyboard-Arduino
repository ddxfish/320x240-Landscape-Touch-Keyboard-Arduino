/* 320x240 Landscape Keyboard

This is code for a landscape mode keyboard on 320x240 displays using the ILI9341 TFT and an XPT2046 touchscreen. 
You must install and set up your config file for TFT_eSPI library to use this.


 This was tested with a cheap red-color touch TFT connected to an ESP32-S3 using SPI.
 The Adafruit TFT uses a different touch chip and likely won't work with this.
 
 Requires TFT_eSPI library
 New users: learn about User_setup and User_setups directory to make it work

 _ means Enter 
 < means Backspace
 
 Created by ddxfish September 2023
 Github: https://github.com/ddxfish/320x240-Landscape-Touch-Keyboard-Arduino
*/
#include <TFT_eSPI.h>

TFT_eSPI tft = TFT_eSPI(); 
String text = ""; 

const char *keys[] = {
  "1234567890",
  "QWERTYUIOP",
  "ASDFGHJKL_",
  "ZXCV BNM-<"
};


int keyW = 30;
int keyH = 30;
int textAreaH = 110;
int spacing = 2;

unsigned long lastPressedTime = 0;

void setup() {
  tft.begin(); 
  tft.setRotation(1); 
  
  drawKeyboard(); 
  drawTextArea(); 
}

void loop() {
  uint16_t x, y;
  if (tft.getTouch(&x, &y, 600)) {
    unsigned long currentMillis = millis();
    if (currentMillis - lastPressedTime > 150) { // 150ms debounce time
      handleTouch(x, y);
      lastPressedTime = currentMillis;
    }
  }
}

void drawKey(int x, int y, const String& label, int width = keyW) {
  tft.fillRect(x, y, width, keyH, TFT_WHITE);
  tft.drawRect(x, y, width, keyH, TFT_BLACK);
  tft.setCursor(x + width / 2 - (label.length() * 6 / 2), y + keyH / 2 - 4);
  tft.setTextColor(TFT_BLACK);
  tft.setTextSize(2); // Change the number to the size you want, 1 is the default size.
  tft.print(label);
}

void drawKeyboard() {
  tft.fillScreen(TFT_BLACK); 
  
  int x = spacing;
  int y = textAreaH + spacing;
  tft.setTextSize(2); // Change the number to the size you want, 1 is the default size.
  for (int row = 0; row < 4; row++) {
    for (int col = 0; col < strlen(keys[row]); col++) {
      drawKey(x, y, String(keys[row][col]));
      x += keyW + spacing;
    }
    x = spacing;
    y += keyH + spacing;
  }
}

void drawTextArea() {
  tft.fillRect(0, 0, 320, textAreaH, TFT_WHITE);
  tft.setCursor(spacing, spacing);
  tft.setTextColor(TFT_BLACK);
  tft.print(text);
}

void handleTouch(uint16_t x, uint16_t y) {
  y = 320-y;
  y=y-90;
  if (y < textAreaH) return;
  
  int row = (y - textAreaH - spacing) / (keyH + spacing);
  int col = x / (keyW + spacing);
  
  if (row == 2 && col == 9){ //enter
    text += '\n';
    drawTextArea();
    return;
  }
  if (row == 3 && col == 9){ //backspace
    if (!text.isEmpty()) text.remove(text.length() - 1);
    drawTextArea();
    return;
  }
  if (row >= 0 && row < 4 && col >= 0 && col < strlen(keys[row])) {
    text += keys[row][col];
    drawTextArea();
    return;
  }

}
