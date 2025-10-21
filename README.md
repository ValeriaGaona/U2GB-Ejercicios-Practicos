# U2GB-Ejercicios-Practicos
## Codigos de ejercicios

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
