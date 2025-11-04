 <img width="919" height="183" alt="image" src="https://github.com/user-attachments/assets/0632f3c5-507a-4b74-aec0-3bab4368ceb5" />

### Universidad Tecnológica del Norte de Guanajuato

### Ingeniería en Tecnologías de la Información e Innovación Digital: Especialización en Desarrollo de Software y Multiplataforma

## Valeria García Gaona (1224100671) - GTID141

# U2GB-Ejercicios-Practicos

#  Tabla de Contenidos

| Documento | Tipo | Evidencia |
|-----------|------|---------|
| Ejercicios practicos de Listas | Códigos | [Ver Códigos](https://github.com/ValeriaGaona/U2GB-Ejercicios-Practicos/blob/main/README.md#ejercicios-practicos-de-listas) |
| Ejercicios practicos de Pilas | Códigos | [Ver Códigos](https://github.com/ValeriaGaona/U2GB-Ejercicios-Practicos/blob/main/README.md#ejercicios-practicos-de-pilas) |
| Ejercicios practicos de Colas | Códigos | [Ver Códigos](https://github.com/ValeriaGaona/U2GB-Ejercicios-Practicos/blob/main/README.md#ejercicios-practicos-de-colas) |


# Ejercicios practicos de Listas

### Ejercicio 1: Manipulación de Lista Enlazada
```
package pilasEjercicos;
import java.util.Random;
import java.util.Scanner;

/**
 *  Ejercicios practicos. Ejercicio 1: Manipulación de Lista Enlazada
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 20/10/25 - 1224100671.vgg@gmail.com
 */
class NodoEntero {
    int dato;
    NodoEntero siguiente; //esta es la referencia al siuiente nodo

    //constructor que inicializa el dato y define al siguiente como null
    public NodoEntero(int dato) {
        this.dato = dato;
        this.siguiente = null;
    }
}

public class ListaNumeros {
    NodoEntero cabeza;

    //método que inserta un nuevo valor al final
    public void push(int valor) {
        NodoEntero nuevo = new NodoEntero(valor);
        //si la lista está vacía, el nuevo nodo es la cabeza
        if (cabeza == null) {
            cabeza = nuevo;
        } else {
            NodoEntero actual = cabeza;
            //recorre hasta el ultimo nodo
            while (actual.siguiente != null) {
                actual = actual.siguiente;
            }
            actual.siguiente = nuevo;
        }
    }

    //mostrar todos los elementos de la lista
    public void peek() {
        NodoEntero actual = cabeza;
        while (actual != null) {
            System.out.print(actual.dato + " ");
            actual = actual.siguiente; //avanza al diguiente nodo
        }
        System.out.println();
    }

    //elimina los nodos al inicio que sean mayores que el límite
    public void pop(int limite) {
        
        while (cabeza != null && cabeza.dato > limite) {
            cabeza = cabeza.siguiente; //mueve la cabeza al siguiente nodo
        }
        NodoEntero actual = cabeza;
        while (actual != null && actual.siguiente != null) {
            if (actual.siguiente.dato > limite) {
                actual.siguiente = actual.siguiente.siguiente; //salta al nodo mayor
            } else {
                actual = actual.siguiente;
            }
        }
    }

    public static void main(String[] args) {
        ListaNumeros lista = new ListaNumeros();
        Random rand = new Random();
        Scanner sc = new Scanner(System.in);

        //inserta los 10 numeros aleatorios
        for (int i = 0; i < 10; i++) {
            lista.push(rand.nextInt(100) + 1);
        }

        System.out.println("Lista original:");
        lista.peek();

        System.out.print("Ingrese el valor límite: ");
        int limite = sc.nextInt(); //lee el limite
        lista.pop(limite); //elimina los mayores que el limite

        System.out.println("Lista después de hacer pop a mayores de " + limite + ":");
        lista.peek(); //muestra la lista
    }
}
```

### Ejercicio 2: Lista Enlazada de Palabras desde Archivo
```
package leerPalabras;

/**
 *  Ejercicios practicos. Ejercicio 2: Lista Enlazada de Palabras desde Archivo
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 03/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.ArrayList;
import java.util.List;
/**
 * Implementación genérica de una lista.
 */
public class lista<T> {
    private Nodo<T> cabeza; //primer nodo

    
    private static class Nodo<T> { //esta clase representa al primer nodo
        T dato;
        Nodo<T> siguiente;

        Nodo(T dato) {
            this.dato = dato;
            this.siguiente = null;
        }
    }

    public Nodo<T> getCabeza() {
        return cabeza;
    }

    public void setCabeza(Nodo<T> cabeza) {
        this.cabeza = cabeza;
    }
    
    public void insertarAlFinal(T dato) {// Inserta un elemento al final
        Nodo<T> nuevo = new Nodo<>(dato);
        if (cabeza == null) {
            cabeza = nuevo;
        } else {
            Nodo<T> actual = cabeza;
            while (actual.siguiente != null) {
                actual = actual.siguiente;
            }
            actual.siguiente = nuevo;
        }
    }
    
    public boolean eliminar(T dato) {// Elimina el primer nodo que contiene el dato ingresado
        if (cabeza == null) return false;

        if (cabeza.dato.equals(dato)) {
            cabeza = cabeza.siguiente;
            return true;
        }

        Nodo<T> actual = cabeza;
        while (actual.siguiente != null && !actual.siguiente.dato.equals(dato)) {
            actual = actual.siguiente;
        }

        if (actual.siguiente != null) {
            actual.siguiente = actual.siguiente.siguiente;
            return true;
        }

        return false;
    }
    
    public void mostrarLista() {// Muestra todos los elemnr¿tos de la lista
        Nodo<T> actual = cabeza;
        System.out.println("\n--- Palabras en la lista ---");
        while (actual != null) {
            System.out.println(actual.dato);
            actual = actual.siguiente;
        }
    }

    // Convertir a lista (para guardar en archivo)
    public List<T> toList() {
        List<T> lista = new ArrayList<>();
        Nodo<T> actual = cabeza;
        while (actual != null) {
            lista.add(actual.dato);
            actual = actual.siguiente;
        }
        return lista;
    }
}
```
```
package leerPalabras;
import java.io.*;
import java.util.List;

/**
 *  Ejercicios practicos. Ejercicio 2: Lista Enlazada de Palabras desde Archivo
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 03/11/25 - 1224100671.vgg@gmail.com
 */
public class archivo<T> {

    /**
     * Guarda los elementos de una lista enlazada en un archivo de texto.
     * Cada elemento se escribe en una línea separada.
     */

    public void guardarEnArchivo(lista<T> lista, String name) {
        List<T> elementos = lista.toList();
        try (PrintWriter writer = new PrintWriter(new FileWriter(name))) {
            for (T elem : elementos) {
                writer.println(elem); //escribe cada apalabra en una linea
            }
            System.out.println("Datos guardados en: " + name);
        } catch (IOException e) {
            System.out.println("Error al guardar: " + e.getMessage());
        }
    }

    /**
     * Lee el contenido de un archivo de texto y lo devuelve como una cadena.
     * Si el archivo no existe, se informa al usuario.
     */

    public String leerArchivo(String nombreArchivo) {
        StringBuilder contenido = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader(nombreArchivo))) {
            String linea;
            while ((linea = reader.readLine()) != null) {
                contenido.append(linea).append("\n");
            }
            System.out.println("Se enconntro el archivo.");
        } catch (IOException e) {
            System.out.println("No se encontro el archivo.");
        }
        return contenido.toString();
    }
}
```
```
package leerPalabras;
import java.io.*;
import java.util.List;

/**
 *  Ejercicios practicos. Ejercicio 2: Lista Enlazada de Palabras desde Archivo
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 03/11/25 - 1224100671.vgg@gmail.com
 */
public class archivo<T> {

    /**
     * Guarda los elementos de una lista enlazada en un archivo de texto.
     * Cada elemento se escribe en una línea separada.
     */

    public void guardarEnArchivo(lista<T> lista, String name) {
        List<T> elementos = lista.toList();
        try (PrintWriter writer = new PrintWriter(new FileWriter(name))) {
            for (T elem : elementos) {
                writer.println(elem); //escribe cada apalabra en una linea
            }
            System.out.println("Datos guardados en: " + name);
        } catch (IOException e) {
            System.out.println("Error al guardar: " + e.getMessage());
        }
    }

    /**
     * Lee el contenido de un archivo de texto y lo devuelve como una cadena.
     * Si el archivo no existe, se informa al usuario.
     */

    public String leerArchivo(String nombreArchivo) {
        StringBuilder contenido = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader(nombreArchivo))) {
            String linea;
            while ((linea = reader.readLine()) != null) {
                contenido.append(linea).append("\n");
            }
            System.out.println("Se enconntro el archivo.");
        } catch (IOException e) {
            System.out.println("No se encontro el archivo.");
        }
        return contenido.toString();
    }
}
```

### Ejercicio 3: Representación y Evaluación de Polinomios con Listas Enlazadas
```
package pilasEjercicos;
/**
 *  Ejercicios practicos. Ejercicio 3: Representación y Evaluación de Polinomios con Listas Enlazadas
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 20/10/25 - 1224100671.vgg@gmail.com
 */
class NodoPolinomio {
    int coeficiente;
    int exponente;
    NodoPolinomio siguiente; //esto es la referencia al siguiente nodo

    public NodoPolinomio(int c, int e) {
        coeficiente = c;
        exponente = e;
        siguiente = null;
    }
}

public class Polinomio {
    NodoPolinomio cabeza; //apunta a la cabeza, el primer termino del polinomio

    //agrega un nuevo nodo 
    public void push(int c, int e) {
        NodoPolinomio nuevo = new NodoPolinomio(c, e);
        if (cabeza == null) {
            cabeza = nuevo; //si ni hay mas terminos, este sera el primero
        } else {
            NodoPolinomio actual = cabeza;
            while (actual.siguiente != null) {
                actual = actual.siguiente;
            }
            actual.siguiente = nuevo; // se conecta al nuevo nodo
        }
    }

    public double evaluar(double x) {
        double resultado = 0;
        NodoPolinomio actual = cabeza;
        
        //recorre todos los terminos
        while (actual != null) {
            resultado += actual.coeficiente * Math.pow(x, actual.exponente);
            actual = actual.siguiente;
        }
        return resultado;
    }

    //muetsra la tabla con valores de X y Y
    public void peek() {
        System.out.println("x\tP(x)");
        for (double x = 0.0; x <= 5.0; x += 0.5) {
            System.out.printf("%.1f\t%.2f\n", x, evaluar(x));
        }
    }

    public static void main(String[] args) {
        //crea el polinomio
        Polinomio p = new Polinomio();
        p.push(3, 4);
        p.push(-4, 2);
        p.push(11, 0);
        //muestra la tabla
        p.peek();
    }
}
```

### Ejercicio 4: Polinomio con Lista Enlazada Circular
```
package pilasEjercicos;
/**
 *  Ejercicios practicos. Ejercicio 4: Polinomio con Lista Enlazada Circular
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 20/10/25 - 1224100671.vgg@gmail.com
 */
class NodoCircular {
    int coeficiente;
    int exponente;
    NodoCircular siguiente; //apunta al siguiente nodo

    //inicializa los valores
    public NodoCircular(int c, int e) {
        coeficiente = c;
        exponente = e;
        siguiente = null;
    }
}

public class PolinomioCircular {
    NodoCircular ultimo; //apunta al ultimo nodo indertado en la lista circular

    //inserta un nuevo nodo
    public void push(int c, int e) {
        NodoCircular nuevo = new NodoCircular(c, e);
        
        //si la lista es vacia el nodo se enlaza a si mismo
        if (ultimo == null) {
            nuevo.siguiente = nuevo;
            ultimo = nuevo;
        } else {
            //inserta el nuevo nodo entre el ultimo y primero
            nuevo.siguiente = ultimo.siguiente;
            ultimo.siguiente = nuevo;
            ultimo = nuevo; //se actualiza al ultimo nodo
        }
    }

    //muestra todos los terminos
    public void peek() {
        if (ultimo == null) return; //si lla lista esta vacia no hace nada
        
        NodoCircular actual = ultimo.siguiente;
        do {
            System.out.print(actual.coeficiente + "x^" + actual.exponente + " ");
            actual = actual.siguiente;
        } while (actual != ultimo.siguiente); //recorre la lista hazta volver aal inicio
        System.out.println();
    }

    public static void main(String[] args) {
        PolinomioCircular pc = new PolinomioCircular();
        pc.push(3, 4);
        pc.push(-4, 2);
        pc.push(11, 0);
        
        //muestra los terminos elnalzados
        pc.peek();
    }
}
```

### Ejercicio 5: Lista Doblemente Enlazada de Caracteres
```
package pilasEjercicos;
import java.util.Scanner;
/**
 *  Ejercicios practicos. Ejercicio 5: Lista Doblemente Enlazada de Caracteres
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 20/10/25 - 1224100671.vgg@gmail.com
 */
class NodoChar {
    char letra;
    NodoChar anterior, siguiente; //es la referencia al nodo anterior y siguiente

    //inicializa el nodo con una letra
    public NodoChar(char letra) {
        this.letra = letra;
    }
}

public class ListaCaracteres {
    NodoChar cabeza; //el primer nodo

    //inserta un nuevo nodo
    public void push(char c) {
        NodoChar nuevo = new NodoChar(c);
        if (cabeza == null) {
            cabeza = nuevo; //si la lista esta vacia, el nuevo nodo es la cabeza
        } else {
            NodoChar actual = cabeza;
            while (actual.siguiente != null) {
                actual = actual.siguiente;
            }
            actual.siguiente = nuevo; //conecta el nuevo nodo al final
            nuevo.anterior = actual;
        }
    }

    //ordena los caracteres
    public void ordenar() {
        boolean cambiado;
        do {
            cambiado = false;
            NodoChar actual = cabeza;
            while (actual != null && actual.siguiente != null) {
                if (actual.letra > actual.siguiente.letra) {
                    char temp = actual.letra;
                    actual.letra = actual.siguiente.letra;
                    actual.siguiente.letra = temp;
                    cambiado = true; //indica que hubo un cambio
                }
                actual = actual.siguiente;
            }
        } while (cambiado); //se repite mientras haya cambios
    }

    //mmuestra los caracteres
    public void peek() {
        NodoChar actual = cabeza;
        while (actual != null) {
            System.out.print(actual.letra + " ");
            actual = actual.siguiente;
        }
        System.out.println(); // ← Aquí se completa la línea faltante
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ListaCaracteres lista = new ListaCaracteres();

        System.out.print("Ingrese una cadena de texto: ");
        String cadena = scanner.nextLine();

        //inserta cada caracter en la lista
        for (int i = 0; i < cadena.length(); i++) {
            lista.push(cadena.charAt(i));
        }

        System.out.println("Lista original:");
        lista.peek();

        //ordena los cracteres
        lista.ordenar();

        System.out.println("Lista ordenada alfabéticamente:");
        lista.peek();

        scanner.close();
    }
}
```


# Ejercicios practicos de Pilas 

### Ejercicio 1: Invertir palabra
```
package pilas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.*;

/**
 * Invierte una palabra usando una pila de caracteres.
 */
public class InversorPalabra {

    public static void ejecutar() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Ingrese una palabra: ");
        String palabra = sc.nextLine();
        Stack<Character> pila = new Stack<>();
        for (char c : palabra.toCharArray()) pila.push(c);
        System.out.print("Invertida: ");
        while (!pila.isEmpty()) System.out.print(pila.pop());
    }

    public static void main(String[] args) {
        ejecutar();
    }
}
```

### Ejercicio 2: Pila de nombres
```
package pilas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.*;

/**
 * Permite ingresar nombres y mostrarlos en orden inverso.
 */
public class NombreInversor {

    public static void mostrarNombresInvertidos() {
        Scanner sc = new Scanner(System.in);
        Stack<String> pila = new Stack<>();
        String nombre;
        while (true) {
            System.out.print("Ingrese un nombre (FIN para salir): ");
            nombre = sc.nextLine();
            if (nombre.equalsIgnoreCase("FIN")) break;
            pila.push(nombre);
        }
        System.out.println("Nombres en orden inverso:");
        while (!pila.isEmpty()) {
            System.out.println(pila.pop());
        }
    }

    public static void main(String[] args) {
        mostrarNombresInvertidos();
    }
}
```

### Ejercicio 3: Decimal a binario
```
package pilas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.*;

/**
 * Convierte un número decimal a binario usando pila.
 */
public class ConversorBinario {

    public static void ejecutar() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Ingrese número: ");
        int num = sc.nextInt();
        Stack<Integer> pila = new Stack<>();
        while (num > 0) {
            pila.push(num % 2);
            num /= 2;
        }
        System.out.print("Binario: ");
        while (!pila.isEmpty()) System.out.print(pila.pop());
    }

    public static void main(String[] args) {
        ejecutar();
    }
}
```

### Ejercicio 4: Balanceo de paréntesis
```
package pilas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.Stack;

/**
 * Verifica si los paréntesis de una expresión están balanceados.
 */
public class BalanceadorParentesis {

    public static boolean estaBalanceada(String expr) {
        Stack<Character> pila = new Stack<>();
        for (char c : expr.toCharArray()) {
            if (c == '(') pila.push(c);
            else if (c == ')') {
                if (pila.isEmpty()) return false;
                pila.pop();
            }
        }
        return pila.isEmpty();
    }

    public static void main(String[] args) {
        System.out.println(estaBalanceada("((2+3)*5)")); // true
        System.out.println(estaBalanceada("((2+3)*5"));  // false
    }
}
```

### Ejercicio 5: 
```

```


# Ejercicios practicos de Colas

### Ejercicio 1: Comparación de Colas
```
package colas;

import java.util.*;

/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
public class ColaComparador {

    /**
     * Compara si dos colas son idénticas en tamaño y orden
     * cola1 primera cola
     * cola2 segunda cola
     * ¿ true si son iguales y false si no
     */
    public static <T> boolean sonIdenticas(Queue<T> cola1, Queue<T> cola2) {
        if (cola1.size() != cola2.size()) return false;

        Iterator<T> it1 = cola1.iterator();
        Iterator<T> it2 = cola2.iterator();

        while (it1.hasNext()) {
            if (!Objects.equals(it1.next(), it2.next())) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Queue<Integer> a = new LinkedList<>(List.of(1, 2, 3));
        Queue<Integer> b = new LinkedList<>(List.of(1, 2, 3));
        System.out.println("¿Son idénticas? " + sonIdenticas(a, b)); // true
    }
}
```

### Ejercicio 2: Simulación de supermercado con carritos y cajas
```
package colas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.*;

/**
 * Simula el flujo de clientes en un supermercado con carritos y cajas.
 */
public class Supermercado {

    private final Queue<Integer> carritos = new LinkedList<>();
    private final List<Queue<Cliente>> cajas = new ArrayList<>();

    public Supermercado(int totalCarritos, int totalCajas) {
        for (int i = 0; i < totalCarritos; i++) carritos.add(i);
        for (int i = 0; i < totalCajas; i++) cajas.add(new LinkedList<>());
    }

    /**
     * Ingresa un cliente al sistema.
     */
    public void ingresarCliente(Cliente cliente) {
        if (carritos.isEmpty()) {
            System.out.println(cliente.getNombre() + " espera por carrito...");
            return;
        }
        cliente.setCarrito(carritos.poll());
        Queue<Cliente> cajaMenor = cajas.stream().min(Comparator.comparingInt(Queue::size)).orElse(cajas.get(0));
        cajaMenor.add(cliente);
        System.out.println(cliente.getNombre() + " se colocó en la caja con menos clientes.");
    }

    /**
     * Procesa el pago de los clientes en cada caja.
     */
    public void procesarPago() {
        for (Queue<Cliente> caja : cajas) {
            if (!caja.isEmpty()) {
                Cliente cliente = caja.poll();
                carritos.add(cliente.getCarrito());
                System.out.println(cliente.getNombre() + " pagó y liberó carrito " + cliente.getCarrito());
            }
        }
    }

    public static void main(String[] args) {
        Supermercado sim = new Supermercado(25, 3);
        for (int i = 0; i < 30; i++) sim.ingresarCliente(new Cliente("Cliente" + i));
        sim.procesarPago();
    }
}
```
```
package colas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
/**
 * Representa un cliente en el supermercado.
 */
public class Cliente {
    private final String nombre;
    private int carrito;

    public Cliente(String nombre) {
        this.nombre = nombre;
    }

    public void setCarrito(int carrito) {
        this.carrito = carrito;
    }

    public int getCarrito() {
        return carrito;
    }

    public String getNombre() {
        return nombre;
    }
}
```

### Ejercicio 3: Simulación de atención al cliente en supermercado 
```
package colas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.*;

/**
 * Simula atención al cliente en supermercado durante 7 horas.
 */
public class SimuladorAtencion {

    private final Queue<Cliente> fila = new LinkedList<>();
    private final List<Queue<Cliente>> cajas = new ArrayList<>();
    private final int tiempoSimulacion = 7 * 60; // 7 horas en minutos
    private int clientesAtendidos = 0;
    private int maxFila = 0;
    private int sumaTamañosFila = 0;
    private int tiempoAperturaCajaExtra = -1;

    public SimuladorAtencion() {
        for (int i = 0; i < 3; i++) cajas.add(new LinkedList<>());
    }

    public void simular() {
        for (int minuto = 0; minuto < tiempoSimulacion; minuto++) {
            fila.add(new Cliente("Cliente" + minuto));
            if (fila.size() > 20 && cajas.size() == 3) {
                cajas.add(new LinkedList<>());
                tiempoAperturaCajaExtra = minuto;
            }

            sumaTamañosFila += fila.size();
            maxFila = Math.max(maxFila, fila.size());

            for (Queue<Cliente> caja : cajas) {
                if (!fila.isEmpty()) {
                    caja.add(fila.poll());
                    clientesAtendidos++;
                }
            }
        }

        mostrarEstadisticas();
    }

    private void mostrarEstadisticas() {
        System.out.println("Total clientes atendidos: " + clientesAtendidos);
        System.out.println("Tamaño medio de la fila: " + (sumaTamañosFila / tiempoSimulacion));
        System.out.println("Tamaño máximo de la fila: " + maxFila);
        System.out.println("Minuto de apertura de la cuarta caja: " +
                (tiempoAperturaCajaExtra >= 0 ? tiempoAperturaCajaExtra : "No se abrió"));
    }

    public static void main(String[] args) {
        new SimuladorAtencion().simular();
    }
}
```
