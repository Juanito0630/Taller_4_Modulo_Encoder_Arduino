# Taller_4_Modulo_Encoder_Arduino

Nombres: Maria Fernanda Lozano Cañon
         Juan Pablo Rodriguez

Reporte de la actividad:

El dia de hoy se realizo el taller de arduino Módulo Encoder/Codificador Rotativo.
Lo que se logro con este taller fue identificar cuando se giraba el codificador en sentido horario se iba aumentando de uno en uno comenzando desde 50 y si se giraba en sentido contrario disminuia, a este se le pusieron limites, en sentido horario llegaba hasta 100 y aunque se siguiera girando en ese sentido no pasaba de 100, en sentido antihorario su tope era 0 y cuando llegaba hasta ahi no seguia disminuyendo

Para esto se declararon dos variables: A y B y a cada una se le dio el valor del puerto en el que estaba conectado a la placa, se declaro una variable ANTERIOR que es la que lleva el conteo del ultimo valor de la variable posicion, se crea la variable POSICION y se le da un valor inicial de 50 este indica la posicion en l que iniciara el conteo.
Se declaran las posiciones y las entradas de los pines en el "void setup" y se le pone un mensaje para confirmar que se conecto correctamente.
En el "void loop" se realiza un funcion if en la cual la condicion sera que si POSICION es diferente de ANTERIOR actualizara ANTERIOR para que sea posible el conteo y se imprimira en la consola.
En "void encoder" se pone un if donde si el valor de B es alto significa que se esta girando en sentido horario haciendo que aumenten los numeros hasta su tope y si no haciendo que disminuyan hasta su tope.

Codigo Actividad:

<code>
         int A = 2;
int B = 4;

int ANTERIOR = 50;

volatile int POSICION = 50;

void setup() {
  pinMode(A, INPUT);
  pinMode(B, INPUT);

  Serial.begin(9600);

  attachInterrupt(digitalPinToInterrupt(A), encoder, LOW);

  Serial.println("Listo"); 
}

void loop() {
  if (POSICION != ANTERIOR){
    Serial.println(POSICION);
    ANTERIOR = POSICION;
  }
}

void encoder() {
  static unsigned long ultimaInterrupcion = 0;
  unsigned long tiempoInterrupcion = millis();

  if (tiempoInterrupcion - ultimaInterrupcion > 5){  

  if (digitalRead(B) == HIGH)
  {
    POSICION++;
  }
  else{ 
    POSICION--;
  }
  POSICION = min(100,max(0,POSICION));

  ultimaInterrupcion = tiempoInterrupcion;
  }
}
</code>
