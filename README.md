
# Blockchain y SHA-256

## Blockchain

### ¿Qué es Blockchain?
Un blockchain es una base de datos distribuida y descentralizada que almacena información en bloques encadenados de forma cronológica e inmutable. Es conocido por su uso en criptomonedas como Bitcoin, pero tiene muchas otras aplicaciones.

#### **Características principales:**
1. **Descentralización:** Los datos se distribuyen en nodos interconectados.
2. **Inmutabilidad:** Una vez que un bloque es validado, no puede modificarse.
3. **Transparencia:** Las transacciones son visibles para los participantes de la red.
4. **Seguridad:** Resistente a manipulaciones gracias a su diseño y la criptografía.

---

## Criptografía en Blockchain

### ¿Qué es SHA-256?
SHA-256 (Secure Hash Algorithm 256-bit) es una función de hash criptográfica que convierte una entrada de cualquier tamaño en una salida de 256 bits (32 bytes). Es unidireccional, lo que significa que no se puede revertir.

### Propiedades clave:
1. **Determinismo:** Produce el mismo hash para la misma entrada.
2. **Salida fija:** Siempre genera una salida de 256 bits.
3. **Resistencia a colisiones:** Difícil encontrar dos entradas diferentes con el mismo hash.
4. **Avalancha:** Un cambio mínimo en la entrada altera drásticamente el hash.

---

## Funcionamiento de SHA-256

### **1. Preprocesamiento**
- **División en bloques:** La entrada se divide en bloques de 512 bits.
- **Padding:** Se añaden bits hasta alcanzar un tamaño de 512 bits, incluyendo la longitud de la entrada original.

### **2. Inicialización**
SHA-256 utiliza 8 constantes iniciales de 32 bits derivadas de fracciones de las raíces cuadradas de números primos.

### **3. Procesamiento**
- Cada bloque de 512 bits se divide en 16 palabras de 32 bits.
- Se expanden a 64 palabras mediante mezclas de rotaciones y desplazamientos.
- Se procesan iterativamente utilizando funciones como:
  - **Ch (Choose):** `(e AND f) XOR (NOT e AND g)`
  - **Maj (Majority):** `(a AND b) XOR (a AND c) XOR (b AND c)`
  - **Sigma0 y Sigma1:** Rotaciones y desplazamientos de bits.

### **4. Actualización**
Los valores finales de cada bloque se suman a las constantes iniciales usando sumas modulares de 32 bits.

### **5. Salida final**
El hash de 256 bits es la concatenación de los valores resultantes.

---

## Ejemplo práctico de SHA-256
Entrada: `hello`
Hash: `2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824`

---

## Aplicaciones
1. **Blockchain:** Enlaza bloques mediante el hash del bloque anterior.
2. **Firmas digitales:** Verifica la integridad de datos.
3. **Contraseñas:** Almacena contraseñas como hashes.
4. **Integridad de archivos:** Asegura que un archivo no ha sido alterado.

---

# Implementación de SHA-256 en Python

Esta implementación de SHA-256 en Python sigue el diseño del algoritmo original, que toma una entrada de cualquier tamaño y produce un resumen (hash) de 256 bits. Este README explica cómo funciona el código, incluyendo cada parte de la implementación.

---

## **Estructura del Algoritmo**

### 1. **Preprocesamiento**
El preprocesamiento incluye:
- **Padding (relleno):** 
  - Añadir un bit "1" al final del mensaje.
  - Rellenar con ceros hasta que la longitud del mensaje sea congruente con 448 bits módulo 512.
  - Añadir la longitud del mensaje original (en bits) como un entero de 64 bits al final.

### 2. **Constantes Iniciales**
- **H:** 8 constantes iniciales derivadas de las raíces cuadradas de los primeros 8 números primos.
- **K:** 64 constantes derivadas de las raíces cúbicas de los primeros 64 números primos.

### 3. **Procesamiento de Bloques**
- Se divide el mensaje en bloques de 512 bits.
- Cada bloque se expande a 64 palabras utilizando operaciones bit a bit como rotaciones y desplazamientos.

### 4. **Compresión**
Se ejecutan 64 rondas de operaciones de mezcla que utilizan funciones auxiliares como:
- `Ch`: Función "elije", basada en AND, NOT y XOR.
- `Maj`: Función "mayoría", basada en AND y XOR.
- `Sigma`: Operaciones de rotación y desplazamiento.

### 5. **Hash Final**
Los valores hash resultantes de todos los bloques se combinan y se convierten en un hash hexadecimal de 256 bits.

---

## **Funciones Importantes**

### **1. `rotate_right(value, shift, size=32)`**
Esta función realiza rotaciones circulares hacia la derecha, necesarias para las operaciones `Sigma` del algoritmo.

### **2. `sha256_compress(chunk, h)`**
Procesa cada bloque de 512 bits, actualizando los valores temporales (`a` a `h`) mediante 64 iteraciones de funciones de mezcla y compresión.

### **3. `sha256(data)`**
Es la función principal que:
- Realiza el preprocesamiento del mensaje.
- Divide el mensaje en bloques.
- Llama a `sha256_compress` para cada bloque.
- Combina los resultados en el hash final.

---

## **Uso del Código**

El código incluye un ejemplo de uso que calcula el hash SHA-256 de la palabra "hello".

```python
if __name__ == "__main__":
    message = b"hello"
    print(f"Mensaje: {message.decode()}")
    print(f"Hash SHA-256: {sha256(message)}")
```

### **Salida del Ejemplo**
```
Mensaje: hello
Hash SHA-256: 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
```

---

## **Requisitos**
Este script solo requiere Python estándar, sin bibliotecas externas.

---

## **Cómo Ejecutarlo**
1. Copia el código a un archivo llamado `sha256.py`.
2. Ejecuta el archivo en un entorno de Python:
   ```
   python sha256.py
   ```
3. Modifica la variable `message` para probar otras entradas.

---

## **Notas Técnicas**
1. La implementación es educativa y no está optimizada para producción.
2. Para un uso práctico, se recomienda utilizar bibliotecas optimizadas como `hashlib` en Python.

---

¡Explora el código y comprende cómo funciona uno de los algoritmos de hash más importantes en la criptografía moderna!
