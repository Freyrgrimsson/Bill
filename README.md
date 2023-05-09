# Bill 
## Skyrsla

Myndband

Slálfkeyrandi bíll með árekstrarvörn. 
Við notuðum parta í bílinn, Arduino IDE, arduino pakkann, og leiðbeiningarnar á Github. 
Einu höfunar og heimildir eru kennararnir og Github-síðan. 

Við gleymdum að taka myndir af bílnum meðan við vorum að smíða hann. 

Kóði fyrir functions:
```c++
// Sonic skynjari
int echoPin = 9;
int trigPin = 10;                                                                    


// Mótor A
int pwmA = 3;
int Ai1 = 5;
int Ai2 = 4;




// Mótor B
int pwmB = 6;
int Bi1 = 7;
int Bi2 = 8;




void setup() {
  // Sonic pinnar
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  // Mótor pinnar
  pinMode(pwmA, OUTPUT);
  pinMode(pwmB, OUTPUT);
  pinMode(Ai1, OUTPUT);
  pinMode(Ai2, OUTPUT);
  pinMode(Bi1, OUTPUT);
  pinMode(Bi2, OUTPUT);
}




void loop() {  
	
  afram(255);
  delay(1000);
  afram(127);
  delay(1000);
  stoppa(0);
  delay(1000);
  haegri(72);
  delay(1000);
  stoppa(0);
  delay(1000);
  bakka(127);
  delay(1000);
  stoppa(0);
  delay(1000);
  vinstri(72);
  delay(1000);
  stoppa(0);
  delay(1000);
  haegri(72);
  delay(1000);
  haegri(72);
  delay(1000);
  stoppa(0);
  delay(1000);


}


// hreyfi function
void bakka(int hradi) {
  // motor A
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  // motor B
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, HIGH);
  //speed  
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void haegri(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  digitalWrite(Bi1, HIGH); // klara her
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void vinstri(int hradi) {
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW); // klara her
  digitalWrite(Bi2, HIGH);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void stoppa(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}


void afram(int hradi) {
  // Set Motor A forward
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  // Set Motor B forward
  digitalWrite(Bi1, HIGH);
  digitalWrite(Bi2, LOW);
  // Set the motor speeds
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}




int maelaFjarlaegd()  {
  // sendir út púlsar
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);




  // mælt hvað púlsarnir voru lengi að berast til baka
  return pulseIn(echoPin,HIGH)/58.0; // deilt með 58 til að breyta í cm
}









```
Kóði fyrir áresktrarvörn:
```c++
// Sonic skynjari
int echoPin = 10;
int trigPin = 9;                                                                    


// Mótor A
int pwmA = 3;
int Ai1 = 5;
int Ai2 = 4;


// slembilukka
long rtala;


// Mótor B
int pwmB = 6;
int Bi1 = 7;
int Bi2 = 8;




void setup() {
  // Sonic pinnar
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  // Mótor pinnar
  pinMode(pwmA, OUTPUT);
  pinMode(pwmB, OUTPUT);
  pinMode(Ai1, OUTPUT);
  pinMode(Ai2, OUTPUT);
  pinMode(Bi1, OUTPUT);
  pinMode(Bi2, OUTPUT);
  Serial.begin(9600);
}




void loop() {  
  afram(200);
  int fj = maelaFjarlaegd();
  Serial.println(fj);
  if(fj < 50) {
    rtala = random(0,2);
    if(rtala == 0)
    {
      haegri(72);
      delay(1000);
      stoppa(0);
      delay(1000);
    }
    if(rtala == 1)
    {
      vinstri(72);
      delay(1000);
      stoppa(0);
      delay(1000);
    }
  }
 
}


// hreyfi function
void bakka(int hradi) {
  // motor A
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  // motor B
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, HIGH);
  //speed  
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void haegri(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  digitalWrite(Bi1, HIGH); // klara her
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void vinstri(int hradi) {
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW); // klara her
  digitalWrite(Bi2, HIGH);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void stoppa(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}


void afram(int hradi) {
  // Set Motor A forward
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  // Set Motor B forward
  digitalWrite(Bi1, HIGH);
  digitalWrite(Bi2, LOW);
  // Set the motor speeds
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}




int maelaFjarlaegd()  {
  // sendir út púlsar
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);




  // mælt hvað púlsarnir voru lengi að berast til baka
  return pulseIn(echoPin,HIGH)/58.0; // deilt með 58 til að breyta í cm
}








```
Kóði fyrir betri árestrarvörn:
```c++
// Sonic skynjari
int echoPin = 10;
int trigPin = 9;                                                                    




// Mótor A
int pwmA = 3;
int Ai1 = 5;
int Ai2 = 4;




// slembilukka
long rtala;




// Mótor B
int pwmB = 6;
int Bi1 = 7;
int Bi2 = 8;








void setup() {
  // Sonic pinnar
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  // Mótor pinnar
  pinMode(pwmA, OUTPUT);
  pinMode(pwmB, OUTPUT);
  pinMode(Ai1, OUTPUT);
  pinMode(Ai2, OUTPUT);
  pinMode(Bi1, OUTPUT);
  pinMode(Bi2, OUTPUT);
  Serial.begin(9600);
}






void loop() {  
  afram(200);
  int fj = maelaFjarlaegd();
  Serial.println(fj);
  if(fj < 50) {
    stoppa(0);
    delay(1000);
    vinstri(75);
    delay(1000);
    int v = maelaFjarlaegd();
    delay(1000);
    haegri(75);
    delay(2000);
    int h = maelaFjarlaegd();
    delay(1000);
    if(v < 50 && h <50){
      haegri(75);
      delay(1000);
    }
    else if(h < v){
      vinstri(75);
      delay(2000);
    }
  }
 
}




// hreyfi function
void bakka(int hradi) {
  // motor A
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  // motor B
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, HIGH);
  //speed  
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void haegri(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, HIGH);
  digitalWrite(Bi1, HIGH); // klara her
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void vinstri(int hradi) {
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW); // klara her
  digitalWrite(Bi2, HIGH);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}
void stoppa(int hradi) {
  digitalWrite(Ai1, LOW);
  digitalWrite(Ai2, LOW);
  digitalWrite(Bi1, LOW);
  digitalWrite(Bi2, LOW);
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}




void afram(int hradi) {
  // Set Motor A forward
  digitalWrite(Ai1, HIGH);
  digitalWrite(Ai2, LOW);
  // Set Motor B forward
  digitalWrite(Bi1, HIGH);
  digitalWrite(Bi2, LOW);
  // Set the motor speeds
  analogWrite(pwmA, hradi);
  analogWrite(pwmB, hradi);
}








int maelaFjarlaegd()  {
  // sendir út púlsar
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);








  // mælt hvað púlsarnir voru lengi að berast til baka
  return pulseIn(echoPin,HIGH)/58.0; // deilt með 58 til að breyta í cm
}


















```
