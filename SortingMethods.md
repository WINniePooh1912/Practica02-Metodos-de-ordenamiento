## Selection sort

El método de ordenamiento por selección consiste en encontrar el elemento de menor (o mayor) valor en cada iteración de la parte desordenada y posicionarlo al inicio del arreglo (o lista) donde se encontrarán los elementos ordenados.

Puede decirse que este método funciona con dos sub-arreglos:

1. El que ya se encuentra ordenado.
2. El que todavía contiene elementos desordenados.

### Pasos.

1. Saber la cantidad de elementos del arreglo.
2. Posicionarnos al inicio del arreglo. Llamemos al valor guardado en esa posición como valor “elegido”.
3. Comparar el valor elegido con los otros elementos, uno por uno, del arreglo.
    
    Cuando se busca ordenar de menor a mayor:
    
    - Si el valor elegido es mayor al valor comparado, entonces el valor comparado se vuelve el valor elegido y el elegido se posiciona donde se encontraba el comparado.
    - Si el valor elegido es menor al valor comparado, entonces el elemento siguiente se vuelve el valor comparado.
    
    Cuando se busca ordenar de mayor a menor:
    
    - Si elegido < comparado → comparado y elegido intercambian posiciones.
    - Si elegido > comparado → comparado = siguiente valor.
4. Se continua comparando hasta que el valor elegido sea el menor (o mayor) y se posiciona en el sub-arreglo ordenado. 

### Complejidad.

**Temporal:** $O(N^2)$

La variable $N$ está elevada al cuadrado porque cuenta con dos ciclos anidados.

- El primer ciclo es para seleccionar un elemento del arreglo.
- El segundo ciclo es para comparar el elemento con cada uno de los restantes.

**Espacial:** $O(1)$

Debido a que la memoria “extra” usada es una única variable “temporal” para poder intercambiar dos valores del arreglo.

Este método de ordenamiento nunca hace más de $O(N)$ intercambios.

### Implementación en código.
```java
public class SelectionSort {
	void sort(int arr[]) {
		int n = arr.length;

		// recorre la posición inicial
		// del sub-arreglo desordenado
		for (int i = 0; i < n-1; i++) {
			// encuentra el valor minimo
			int min = i;
			for (int j = i+1; j < n; j++)
				if (arr[j] < arr[min])
					min = j;

			// intercambia el valor mínimo
			// con la posición inicial del
			// sub-arreglo desordenado
			int temp = arr[min];
			arr[min] = arr[i];
			arr[i] = temp;
		}
	}

	// muestra el arreglo
	void printArray(int arr[]) {
		int n = arr.length;

		for (int i = 0; i < n; ++i)
			System.out.print(arr[i]+" ");
		System.out.println();
	}
}
```
## Bubble sort

El método de ordenamiento “burbuja” consiste en repetidamente intercambiar los elementos adyacentes si están en el orden incorrecto. Este método se encarga de ordenar desde el final del arreglo hasta el inicio, en otras palabras, el primer valor que posiciona en el lugar correcto está en la última posición del arreglo.

### Pasos.

1. Saber la cantidad de elementos del arreglo.
2. Posicionarnos al inicio del arreglo. Llamemos al valor guardado en esa posición como valor “dato”.
3. Guardamos el valor adyacente (próximo) como “siguiente”.
4. Comparar “dato” con “siguiente”.
    
    Cuando se busca ordenar de menor a mayor:
    
    - Si dato > siguiente → siguiente y dato intercambian posiciones.
    - Si dato < siguiente → dato = siguiente.
    
    Cuando se busca ordenar de mayor a menor:
    
    - Si dato < siguiente → siguiente y dato intercambian posiciones.
    - Si dato > siguiente → dato = siguiente.
5. Se continua comparando hasta que el dato sea el menor (o mayor) y se posicione en el último nivel disponible del arreglo. 

### Complejidad.

**Temporal:** $O(N^2)$

La variable $N$ está elevada al cuadrado porque cuenta con dos ciclos anidados.

- El primer ciclo es para recorrer el arreglo las veces necesarias $(N - 1)$.
- El segundo ciclo es para intercambiar (o no) las posiciones de los elementos del arreglo.

**Espacial:** $O(1)$

Debido a que la memoria “extra” usada es una única variable “temporal” para poder intercambiar dos valores del arreglo.

### Implementación en código.

```java
public class BubbleSort {
    static void bubbleSort(int arr[], int n) {
        int position, data, temp;
        boolean swapped;

        for (position = 0; position < n - 1; position++) {
            swapped = false;
            for (data = 0; data < n - position - 1; data++) {
                if (arr[data] > arr[data + 1]) {

                    // intercambio de elementos
                    temp = arr[data];
                    arr[data] = arr[data + 1];
                    arr[data + 1] = temp;
                    swapped = true;
                }
            }

            // si no hay intercambio
            if (swapped == false)
                break;
        }
    }

    // muestra el arreglo
    static void printArray(int arr[], int size) {
        int i;

        for (i = 0; i < size; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }
}
```
## Insertion sort

El método de ordenamiento por inserción consiste en dividir el arreglo en dos partes, una ordenada y otra desordenada. Los valores de la parte desordenada son tomados y mandados a la ordenada. 

Este método va ordenado los valores conforme recorre el arreglo, una y otra vez hasta que termina.

### Pasos.

1. Saber la cantidad de elementos del arreglo.
2. Posicionarnos en el primer elemento del arreglo. Llamemos al valor guardado en esa posición como valor “elegido”.
3. Comparar el valor elegido con el elemento siguiente e intercambiarles la posición de ser necesario. Dejando la posición del valor “elegido” como el último valor del arreglo ordenado.
4. Recorrer, en una posición, el valor “elegido” y volver al paso anterior.
    - Si el valor “siguiente” es menor al primer valor, usando un ciclo, se acomoda el valor en su posición correcta.

### Complejidad.

**Temporal:** $O(N^2)$

La variable $N$ está elevada al cuadrado porque cuenta con dos ciclos anidados.

- El primer ciclo es para seleccionar un elemento del sub-arreglo desordenado e intercambiar su posición con el adyacente (de ser necesario).
- El segundo ciclo es para acomodar los elementos en el sub-arreglo de los ordenados.

En el mejor de los casos, la complejidad de tiempo es de $O(N)$.

**Espacial:** $O(1)$

Debido a que la memoria “extra” usada es una única variable “temporal” para poder intercambiar dos valores del arreglo.

### Implementación en código.

```java
public class InsertionSort {
    void sort(int arr[]) {
        int n = arr.length;

        for (int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;

			// mueve los elementos del arreglo
			// que son mayores que "key" a una
			// posición anterior a la actual

            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }

            arr[j + 1] = key;
        }
    }

	// muestra el arreglo
    static void printArray(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
    }
}
```