# CONECTA4
## CODEWARS KYU5 KATA
### TAREA
El juego consta de una cuadrícula (7 columnas y 6 filas) y dos jugadores que se turnan para dejar caer sus fichas. Las piezas caen hacia abajo, ocupando el siguiente espacio disponible dentro de la columna. El objetivo del juego es ser el primero en formar una línea horizontal, vertical o diagonal de cuatro fichas propias.

Tu tarea es crear una clase llamada Connect4 que tenga un método llamado *play* que toma un argumento para la columna donde el reproductor colocará su ficha.
### REGLAS
1. Si un jugador tiene con éxito 4 fichas en horizontal, vertical o diagonal, entonces return: "¡El jugador n gana!". donde n es el jugador actual 1 o 2.

3. Si un jugador intenta colocar una ficha en una columna que está llena, deberá devolver "¡Columna llena!". y el siguiente movimiento debe ser realizado por el mismo jugador.

5. Si un jugador ganó el juego, cualquier movimiento siguiente debería devolver "¡El juego ha terminado!".

7. Cualquier otro movimiento debería devolver "El jugador n tiene un turno", donde n es el jugador actual, ya sea 1 o 2.

9. El jugador 1 comienza el juego cada vez y se alterna con el jugador 2.

11. Las columnas están numeradas del 0 al 6 de izquierda a derecha.

 ### CÓDIGO

```java
public class Connect4 {
   int [][] tablero = new int [6][7];  
   int jugador = 2; // turno actual
   boolean fin = false; //terminar partida
   int columnaActual =0;
   int filaActual = 0;
   

  public String play(int column) { //FUNCION PLAY 
    if (fin) {
      return "Game has finished!" ; //termina el juego
    } 
    
    jugador= jugador == 1 ? 2 : 1 ; //Control de turnos
    
    for (int i = 5; i >= 0; i--) { //Comprobamos si podemos colocar la ficha 
      if(tablero[i][column] == 0) {
        tablero[i][column] = jugador;
        columnaActual = column;
        filaActual = i;
        break;
      }
    if(i == 0) { // Si no cabe la ficha, devuelvo columna llena y sigue jugando el mismo jugador
        jugador = jugador == 1 ? 2 : 1;
        return "Column full!";
      }
    }
    if(Ganador(columnaActual, filaActual)) { // Comprobamos las wincon en los metodos 
      fin = true;
      return "Player " + jugador + " wins!";
    }
    
    return "Player " + jugador  + " has a turn"; //Si no ha terminado el juego, cambio de turno

  }
  
  
  private boolean Ganador(int column, int row) { //Comprobamos si hay ganador
    
    if(ComprobarVertical(column) || ComprobarHorizontal(row) || ComprobarDiagonalD() || ComprobarDiagonalI()) {
      return true;
    } else {
      return false;
    }
  }
  
  private boolean ComprobarVertical(int column) { //Comprobamos combinación vertical
    
    for (int i = 2; i >= 0; i--) {
      if ((tablero[i][column] != 0) && (tablero[i][column] == tablero[i+1][column]) && (tablero[i+1][column] == tablero[i+2][column]) && (tablero[i+2][column] == tablero[i+3][column])){
        return true;
      }
    }
    
    return false;
  }
  
  private boolean ComprobarHorizontal(int row) { //Comprobamos combinación horizontal
    
    for (int i = 0; i <= 3; i++) {
      if ((tablero[row][i] != 0) &&  (tablero[row][i] == tablero[row][i+1]) &&  (tablero[row][i+1] == tablero[row][i+2]) && (tablero[row][i+2] == tablero[row][i+3])){
        return true;
        }
      }
    
    return false;
  }
  
  private boolean ComprobarDiagonalD() { //Comprobamos combinación diagonal derecha 
    
    for (int i = 2; i >= 0; i--) {
      for (int j = 0; j <= 3; j++) {
        if ((tablero[i][j] != 0) &&  (tablero[i][j] == tablero[i+1][j+1]) &&  (tablero[i+1][j+1] == tablero[i+2][j+2]) && (tablero[i+2][j+2] == tablero[i+3][j+3])) {
          return true;
        }
      }
    }
    
    return false;
  }
      
  private boolean ComprobarDiagonalI() { //Comprobamos  combinación diagonal izquierda
    
    for (int i = 5; i >= 3; i--) {
      for (int j = 0; j <= 3; j++) {
        if ((tablero[i][j] != 0) &&  (tablero[i][j] == tablero[i-1][j+1]) && (tablero[i-1][j+1] == tablero[i-2][j+2]) && (tablero[i-2][j+2] == tablero[i-3][j+3])) {
          return true;
        }
      }
    }
    
    return false;
  }
  
}
```
### ENLACE AL KATA
[Conecta4 Link](https://www.codewars.com/kata/586c0909c1923fdb89002031 "Conecta4 Link")
