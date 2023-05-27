#include <Adafruit_NeoPixel.h>

#define PIN 6	 // input pin Neopixel is attached to

#define NUMPIXELS      143 // number of neopixels in strip

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);


boolean button_right = !digitalRead(1);
boolean button_left = !digitalRead(2);


int score_left = 0;
int score_right = 0;

uint32_t red = pixels.Color(255, 0, 0);
uint32_t white = pixels.Color(255, 255, 255);

int arr[] = {-1, 1};

void setup() {
  
  pinMode(1, INPUT_PULLUP);
  pinMode(2, INPUT_PULLUP);
  Serial.begin(9600);
  pixels.begin();
}

void re_game(){
  for (int i=0; i < NUMPIXELS/2 + 1; i++) {
    if (i == NUMPIXELS/2){
      pixels.setPixelColor(NUMPIXELS/2, red);
 
    }
    else{
      pixels.setPixelColor(i, white);
      pixels.setPixelColor(NUMPIXELS - i-1, white);
    } 
    pixels.show();

    delay(20);
  }
  
  delay(100);
 
}

void start_game(){
  int num = rand();
  int side = arr[num%2];
  for (int i = 0; i < NUMPIXELS/2 + 1; i++){
    button_right = !digitalRead(1);
    button_left = !digitalRead(2);
    int index_1 = NUMPIXELS/2 + side*i;
    int index_2 = NUMPIXELS/2 + side*(i - 1);
    if (index_1 == 0){
      pixels.setPixelColor(index_1, red);
      pixels.setPixelColor(index_2, white);
      pixels.show();
      delay(100);
      score_right++;
      pixels.fill(0xFF0000, 0, 72);
      pixels.fill(0x00FF00, 72, 144);
      pixels.show();
      delay(700);
      break;
    }
    if (index_1 == NUMPIXELS - 1){
      pixels.setPixelColor(index_1, red);
      pixels.setPixelColor(index_2, white);
      pixels.show();
      delay(100);
      score_left++;
      pixels.fill(0xFF0000, 72, 144);
      pixels.fill(0x00FF00, 0, 72);
      pixels.show();
      delay(700);
      break;
    }
    
    pixels.setPixelColor(index_1, red);
    pixels.setPixelColor(index_2, white);
    
    pixels.show();
    delay(30); 
    if (button_right == 1 and index_1 > NUMPIXELS/2){
      game(index_1, index_2, index_1);
      break;
    }
    
    if (button_left == 1 and index_1 <= NUMPIXELS/2){
      game(index_1, index_2, index_1);
      break;
    }
  }
}

void game(int index_1, int index_2, int reverse){
  int speed = 0;
  if (button_right == 1 and index_1 > NUMPIXELS/2){
    button_right = !digitalRead(1);
    for (int j = 0; j < index_1 + 1; j++){
      button_left = !digitalRead(2);
      int ind = index_1 - j;
      if (ind == 0){
        pixels.setPixelColor(ind, red);
        pixels.setPixelColor(ind + 1, white);
        pixels.show();
        delay(70);
        score_right++;
        pixels.fill(0xFF0000, 0, 72);
        pixels.fill(0x00FF00, 72, 144);
        pixels.show();
        delay(300);
        break;
      }
      if (button_left == 1 and ind <= NUMPIXELS/2){
        game(ind-1, ind, ind);
        break;
      }
      
      else{
        pixels.setPixelColor(ind, red);
        pixels.setPixelColor(ind + 1, white);
        pixels.show();
        if (NUMPIXELS - reverse > 50){
          delay(120 - speed);
          speed ++;

        }
        else{
          delay(NUMPIXELS - reverse);

        }
      }
    }
  }
  if (button_left == 1 and index_1 < NUMPIXELS/2){
    button_left = !digitalRead(2);
    for (int j = 0; j < NUMPIXELS - index_2; j++){
      button_right = !digitalRead(1);
      int ind = index_2 + j;
      if (ind == NUMPIXELS - 1){
        pixels.setPixelColor(ind, red);
        pixels.setPixelColor(ind - 1, white);
        pixels.show();
        delay(70);
        score_left++;
        pixels.fill(0xFF0000, 72, 144);
        pixels.fill(0x00FF00, 0, 72);
        pixels.show();
        delay(300);
        break;
      }
      if (button_right == 1 and ind >= NUMPIXELS/2){
        game(ind, ind+1, ind);
        break;
      }
      else {
        pixels.setPixelColor(ind, red);
        pixels.setPixelColor(ind - 1, white);
        pixels.show();
        if (reverse > 50){
          delay(120 - speed);
          speed ++;          
        }
        else{
          delay(reverse);

        }
      }
    }
  }
}


void loop() { 
  
  while (score_left < 11 and score_right < 11){
    
    re_game();
    start_game();
    
    pixels.clear();
    pixels.show();
  
  }
  if (score_left > score_right){
    for (int i=0; i < 8; i++) {
      pixels.fill(0xFF0000, 72, 144);
      pixels.fill(0x00FF00, 0, 72);
      pixels.show();
      delay(100);
      pixels.clear();
      pixels.show();
      delay(50);
    }
  }
  else{
    for (int i=0; i < 8; i++) {
      pixels.fill(0xFF0000, 0, 72);
      pixels.fill(0x00FF00, 72, 144);
      pixels.show();
      delay(100);
      pixels.clear();
      pixels.show();
      delay(50);
    }

  }
  pixels.clear();

  score_left = 0;
  score_right = 0;
   
}
