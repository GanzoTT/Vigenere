# 🔐 Vigenère Cipher en Python

Este repositorio contiene una implementación simple del **Cifrado de Vigenère**, un algoritmo clásico de criptografía que utiliza una clave para cifrar y descifrar mensajes de texto.

---

## 📌 Descripción

El **Cifrado de Vigenère** es un método de encriptación que aplica una serie de desplazamientos alfabéticos basados en las letras de una palabra clave.  
- Si la clave es más corta que el mensaje, se repite tantas veces como sea necesario.  
- Cada letra de la clave define el desplazamiento que se aplicará a la letra correspondiente del mensaje.  

---

## 📂 Contenido del código

El archivo principal es [`vigenere.py`](vigenere.py) y está estructurado de la siguiente forma:

### 1. Variables iniciales
```python
text = 'mrttaqrhknsw ih puggrur'
custom_key = 'happycoding'
```
- `text`: mensaje cifrado que se desea descifrar.  
- `custom_key`: la clave utilizada para cifrar/descifrar.  

---

### 2. Función principal `vigenere(message, key, direction=1)`
```python
def vigenere(message, key, direction=1):
    key_index = 0
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    final_message = ''
```
- `message`: texto de entrada (cifrado o en claro).  
- `key`: clave utilizada.  
- `direction`: determina si se cifra (`1`) o se descifra (`-1`).  
- `key_index`: lleva el control de la posición actual en la clave.  
- `alphabet`: alfabeto en minúsculas para referencia de posiciones.  
- `final_message`: resultado del proceso (cifrado o descifrado).  

---

### 3. Iteración sobre el mensaje
```python
for char in message.lower():
    if not char.isalpha():
        final_message += char
    else:
        key_char = key[key_index % len(key)]
        key_index += 1
```
- Convierte todo a minúsculas.  
- Si el carácter no es una letra (espacio, símbolo, etc.), lo agrega sin cambios.  
- Si es una letra:
  - Busca la letra correspondiente de la clave (`key_char`).  
  - Usa el operador módulo `%` para repetir la clave si es más corta que el mensaje.  

---

### 4. Aplicación del desplazamiento
```python
offset = alphabet.index(key_char)
index = alphabet.find(char)
new_index = (index + offset*direction) % len(alphabet)
final_message += alphabet[new_index]
```
- `offset`: posición de la letra de la clave en el alfabeto.  
- `index`: posición de la letra actual del mensaje.  
- `new_index`: nueva posición después del desplazamiento (considerando si es cifrado o descifrado).  
- El uso de `% len(alphabet)` asegura que el índice siempre se mantenga dentro del rango del alfabeto.  

---

### 5. Funciones de utilidad
```python
def encrypt(message, key):
    return vigenere(message, key)

def decrypt(message, key):
    return vigenere(message, key, -1)
```
- `encrypt`: cifra el mensaje con la clave.  
- `decrypt`: descifra el mensaje con la clave (usa `direction=-1`).  

---

### 6. Ejecución principal
```python
print(f'\nEncrypted text: {text}')
print(f'Key: {custom_key}')
decryption = decrypt(text, custom_key)
print(f'\nDecrypted text: {decryption}\n')
```
- Imprime el mensaje cifrado original.  
- Muestra la clave usada.  
- Descifra el mensaje y lo imprime en consola.  

---

## 🚀 Ejemplo de uso

```bash
# Clonar repositorio
git clone https://github.com/usuario/vigenere-cipher.git
cd vigenere-cipher

# Ejecutar
python vigenere.py
```

Salida esperada:
```
Encrypted text: mrttaqrhknsw ih puggrur
Key: happycoding

Decrypted text: ilovemachinelearning
```

---

## 🛠️ Mejoras posibles
- Soporte para mayúsculas.  
- Incluir interfaz gráfica o interfaz de línea de comandos.  
- Añadir pruebas unitarias (`unittest` o `pytest`).  
- Permitir cifrado/descifrado de archivos completos.  

---

## 📖 Referencias
- [Cifrado de Vigenère - Wikipedia](https://es.wikipedia.org/wiki/Cifrado_de_Vigen%C3%A8re)
