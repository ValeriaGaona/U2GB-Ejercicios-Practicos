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

### Ejercicio 5: Verifica si una pila está 
```
package pilas;
/**
 *  Ejercicios practicos.
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 04/11/25 - 1224100671.vgg@gmail.com
 */
import java.util.Stack;

/**
 * Verifica si esta vacía antes y después de insertar elementos.
 */
public class VerificadorVacio {

    public static void ejecutar() {
        Stack<Integer> pila = new Stack<>();
        System.out.println("¿Está vacía la pila? " + pila.isEmpty());
        pila.push(1);
        System.out.println("¿Está vacía la pila? " + pila.isEmpty());
    }

    public static void main(String[] args) {
        ejecutar();
    }
}
```


# Ejercicios practicos de Colas
```
package ec;
/**
 * Ejercicios Colas
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */

class Cola<T> {
    private class Nodo {
        T dato;
        Nodo sig;

        Nodo(T dato) { this.dato = dato; }
    }

    private Nodo frente;
    private Nodo fin;
    private int tamaño;

    /**
     * Metodo para insertar un elemento al final de la cola  
     */
    public void encolar(T dato) {
        Nodo nuevo = new Nodo(dato);
        if (fin != null) fin.sig = nuevo;
        else frente = nuevo;
        fin = nuevo;
        tamaño++;
    }

    /**
     * metodo para quitar y mostrar el elemento del frente  
     */
    public T desencolar() {
        if (frente == null) return null;
        T dato = frente.dato;
        frente = frente.sig;
        if (frente == null) fin = null;
        tamaño--;
        return dato;
    }

    /**
     * Indica si la cola esta vacia  
     */
    public boolean esVacia() {
        return frente == null;
    }

    /**
     *   Muestra el tamaño actual de la cola
     */
    public int tamaño() {
        return tamaño;
    }
    
    /**
     * muestra el elemento del frente sin eliminarlo  
     */
    public T verFrente() {
        return (frente != null) ? frente.dato : null;
    }
}
```

### Ejercicio 1: Comparación de Colas
```
package ec;
/**
 * Ejercicio 1: Comparación de dos colas
 * La comparación preserva el estado original de ambas colas.
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */
public class Comparacion {

    /**
     * Compara dos colas sin modificar su contenido.
     */
    public static <T> boolean compararColas(Cola<T> c1, Cola<T> c2) {
        
        /**
        * Si los tamaños son distintos retorna false  
        */
        if (c1.tamaño() != c2.tamaño()) return false;

        Cola<T> aux1 = new Cola<>();
        Cola<T> aux2 = new Cola<>();

        boolean iguales = true;

        /**
        * Recorre las dos colas a la vez  
        */
        while (!c1.esVacia()) {
            T d1 = c1.desencolar();
            T d2 = c2.desencolar();

            if (!d1.equals(d2)) iguales = false;

            aux1.encolar(d1);
            aux2.encolar(d2);
        }

        // Regresar los elementos a las colas originales
        while (!aux1.esVacia()) c1.encolar(aux1.desencolar());
        while (!aux2.esVacia()) c2.encolar(aux2.desencolar());

        return iguales;
    }

    public static void main(String[] args) {
        Cola<Integer> a = new Cola<>();
        Cola<Integer> b = new Cola<>();

        a.encolar(1); a.encolar(2); a.encolar(3);
        b.encolar(1); b.encolar(2); b.encolar(3);

        System.out.println("¿Son iguales?: " + compararColas(a, b));
    }
}

```

### Ejercicio 2: Simulación de supermercado con carritos y cajas
```
package ec;
/**
 * Ejercicio 2 Colas
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */
/**
* cliente y tiempo en caja  
*/
class Cliente {
    int tiempoServicio;

    Cliente(int servicio) { this.tiempoServicio = servicio; }
}
```
```
package ec;
/**
 * Ejercicio 2 Colas: Simulación de supermercado con carritos
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */
public class SimulacionCarritos {

    public static void main(String[] args) {

        /**
        * Clientes que esperan por un carrito  
        */
        Cola<Cliente> esperandoCarrito = new Cola<>();
        Cola<Cliente> caja1 = new Cola<>();
        Cola<Cliente> caja2 = new Cola<>();
        Cola<Cliente> caja3 = new Cola<>();
        /**
        * Carritos disponibles  
        */
        Cola<Integer> carritos = new Cola<>();

        // Agregar 25 carritos
        for (int i = 1; i <= 25; i++) carritos.encolar(i);

        int minutos = 180; // 3 horas simuladas

        for (int minuto = 0; minuto < minutos; minuto++) {

            // Llega nuevo cliente
            Cliente nuevo = new Cliente((int)(Math.random()*5) + 2); // tiempo 2–6 minutos
            esperandoCarrito.encolar(nuevo);

            // Asignar carritos si hay
            if (!carritos.esVacia()) {
                Cliente c = esperandoCarrito.desencolar();
                carritos.desencolar(); // usa carrito

                // Escoge la caja más corta
                Cola<Cliente> destino = caja1.tamaño() <= caja2.tamaño() ?
                        (caja1.tamaño() <= caja3.tamaño() ? caja1 : caja3)
                        : (caja2.tamaño() <= caja3.tamaño() ? caja2 : caja3);

                destino.encolar(c);
            }

            // Procesar cada caja (disminuir tiempo del cliente frontal)
            procesarCaja(caja1, carritos);
            procesarCaja(caja2, carritos);
            procesarCaja(caja3, carritos);
        }
    }

    static void procesarCaja(Cola<Cliente> caja, Cola<Integer> carritos) {
        if (!caja.esVacia()) {
            Cliente atendiendo = caja.desencolar();
            atendiendo.tiempoServicio--;

            if (atendiendo.tiempoServicio > 0)
                caja.encolar(atendiendo); // regresa a la fila

            else carritos.encolar(1); // libera carrito
        }
    }
}

```


### Ejercicio 3: Simulación de atención al cliente en supermercado 
```
package ec;
/**
 * Ejercicio 3 Colas
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */
class Cliente3 {
    int tiempoLlegada;   // en qué minuto llegó
    int tiempoServicio;  // tiempo total que tarda su atención

    
    Cliente3(int llegada, int servicio) {
        tiempoLlegada = llegada;
        tiempoServicio = servicio;
    }
}
```
```
package ec;
/**
 * Ejercicio 3 Colas: Simulación de atención al cliente con 3 y 4 cajas
 * Ejercicios Practicos U2
 * @author Valeria García Gaona - GTID141 - 1224100671 - Fecha 16/11/25 - 1224100671.vgg@gmail.com
 */
public class SimulacionAtencionClientes {

    public static void main(String[] args) {

        Cola<Cliente3> fila = new Cola<>();
        Cola<Cliente3> c1 = new Cola<>();
        Cola<Cliente3> c2 = new Cola<>();
        Cola<Cliente3> c3 = new Cola<>();
        Cola<Cliente3> c4 = new Cola<>();

        int tiempoSimulacion = 7 * 60; // 7 horas
        int totalAtendidos = 0;
        int maxFila = 0;
        int sumaTamaños = 0;
        int minutosConCaja4 = 0;
        int maxEspera = 0;

        for (int minuto = 0; minuto < tiempoSimulacion; minuto++) {

            // Llega un cliente por minuto
            fila.encolar(new Cliente3(minuto, tiempoAleatorio()));

            // Activar caja 4 si fila > 20
            boolean caja4Activa = fila.tamaño() > 20;
            if (caja4Activa) minutosConCaja4++;

            // Pasar clientes a cajas disponibles
            asignarCaja(c1, fila, minuto);
            asignarCaja(c2, fila, minuto);
            asignarCaja(c3, fila, minuto);
            if (caja4Activa) asignarCaja(c4, fila, minuto);

            // Procesar cajas
            totalAtendidos += procesar(c1);
            totalAtendidos += procesar(c2);
            totalAtendidos += procesar(c3);
            if (caja4Activa) totalAtendidos += procesar(c4);

            // Estadísticas
            sumaTamaños += fila.tamaño();
            maxFila = Math.max(maxFila, fila.tamaño());

            // Cálculo correcto de tiempo de espera
            Cliente3 primero = fila.verFrente();
            if (primero != null) {
                int espera = minuto - primero.tiempoLlegada;
                maxEspera = Math.max(maxEspera, espera);
            }
        }

        /**
        * Se muestran los resultados  
        */
        System.out.println("===== RESULTADOS =====");
        System.out.println("Clientes atendidos: " + totalAtendidos);
        System.out.println("Tamaño máximo de la fila: " + maxFila);
        System.out.println("Tamaño medio: " + (sumaTamaños / (double) tiempoSimulacion));
        System.out.println("Tiempo máximo de espera: " + maxEspera + " minutos");
        System.out.println("Tiempo con caja 4 abierta: " + minutosConCaja4 + " minutos");
    }

    static int tiempoAleatorio() {
        return (int)(Math.random() * 6) + 3; // atención de 3–8 minutos
    }

    /**
     * Si la caja está vacía y hay clientes en la fila, mueve al primero de la fila a la caja  
     */
    static void asignarCaja(Cola<Cliente3> caja, Cola<Cliente3> fila, int minuto) {
        if (caja.esVacia() && !fila.esVacia()) {
            Cliente3 c = fila.desencolar();
            c.tiempoLlegada = minuto - c.tiempoLlegada; // tiempo total en espera
            caja.encolar(c);
        }
    }

    static int procesar(Cola<Cliente3> caja) {
        if (caja.esVacia()) return 0;

        Cliente3 c = caja.desencolar();
        c.tiempoServicio--;

        if (c.tiempoServicio > 0) {
            caja.encolar(c); // sigue siendo atendido
        } else {
            return 1; // cliente atendido por completo
        }
        return 0;
    }
}

```

