# 🦈 hello-tiburona-rust
¡Un saludo de Tamara! 

## Estructura del proyecto

El repositorio tiene la siguiente estructura:
```text
.
├── contracts
│   └── hello_world
│       ├── src
│       │   ├── lib.rs
│       │   └── test.rs
│       └── Cargo.toml
├── Cargo.toml
└── README.md
```

Antes de iniciar, quiero compartir mis reflexiones personales del proceso (La tarea de encuentra al 70%, no he podido implementar pruebas):

## 🏄‍♀️ ¿Qué fue lo más retador?
Que mi version de SDK no es compatible con el codigo de la tarea entonces tuve que hacer algunas modificaciones. 

## 🐇 ¿Qué aprendiste que no esperabas?
Paciencia con los errores y seguir adelante! Hice bastantes anotaciones de recordatorios. 
¡Aprendi a hacer un readme y subir el repo sola a GitHub! Espero haberlo subido bien. 



# 🚀 FASE 1: Verificación de instalaciones y creación del proyecto
🔧 Verificar instalaciones

SOROBAN instalado:
Tuve que instalar Soroban CLI con:


cargo install --locked soroban-cli
soroban --version

RUST instalado:
Ya lo tenía previamente:

rustc --version

😊 Crear el proyecto

Paso 1.1

mkdir proyectos-soroban
cd proyectos-soroban
soroban contract init hello-tiburona
cd hello-tiburona


Paso 1.2: Verificar estructura
En PowerShell ls no funcionó, así que usé Git Bash.

📸 Capturas:
<img width="877" height="448" alt="image" src="https://github.com/user-attachments/assets/5dd3c78f-94f8-4cbd-9035-1cbe5b81b9aa" />
<img width="846" height="318" alt="image" src="https://github.com/user-attachments/assets/563d122d-f3c1-4e08-8c75-632cd995b070" />

### Checkpoint 1 ✅

Proyecto creado

VS Code abierto

Carpeta contracts/ visible

# 🧱 FASE 2: Implementar las definiciones base
## Paso 2.1: Abrir lib.rs

💡 ¿Por qué cada error tiene un número?
Para usarlos como índice (por ejemplo, “error 3”).

💡 ¿Qué error usarías si alguien intenta resetear el contador sin ser admin?
NoAutorizado.

Paso 2.4: Definir DataKey
pub → el enum es público y puede usarse fuera del módulo.
enum DataKey → define un tipo con varias variantes.

💡 ¿Por qué Admin no tiene parámetros, pero UltimoSaludo sí?
Admin es un dato global único, mientras que UltimoSaludo puede cambiar.

### Checkpoint 2 ✅

Imports correctos (incluyendo String)

4 errores definidos

3 keys en DataKey

Estructura creada

Compila con cargo check

💬 Al principio no compilaba, pero corregí typos y comas faltantes. 

# ⚙️ FASE 3: Implementar initialize()
Paso 3.1: Firma de la función

💡 ¿Por qué retorna Result<(), Error> y no solo ()?
Porque incluir el error facilita entender qué salió mal.

💡 ¿Qué podría fallar en una inicialización?
Que alguien intente inicializar el contrato con otra cuenta.

Paso 3.2 - 3.6

💡 ¿Por qué usar instance storage para Admin?
Para guardar el valor asociado al contrato.

💡 ¿Qué significan los dos 100?
Son unidades de tiempo para el TTL (Time To Live).


#### Checkpoint 3 ✅

initialize() implementada

Verifica si ya está inicializado

Guarda admin y contador

Extiende TTL

Compila sin errores

# 💬 FASE 4: Implementar hello()

💡 ¿Por qué retorna Result<Symbol, Error> y no solo Symbol?
Para manejar errores de forma controlada y segura.

💡 ¿Por qué validar la longitud antes de tocar storage?
Porque los errores en blockchain cuestan dinero, así que se evita trabajo innecesario.


### Checkpoint 4 ✅

hello() implementada

2 validaciones de input

Contador incrementado

Saludo guardado

TTL extendido

Compila sin errores

# 🔍 FASE 5: Funciones de consulta
Recordatorios importantes

⭐ La flecha (->) indica el tipo de valor que se retorna.
⭐ unwrap() extrae el valor de un Option.
⭐ Option vs Result:

Option → algo puede o no existir (no es error).

Result → algo puede fallar y queremos saber por qué.

Ejemplo:

pub fn get_contador(env: Env) -> u32 {
    env.storage()
        .instance()
        .get(&DataKey::ContadorSaludos)
        .unwrap_or(0) // No hay error
}

### Checkpoint 5 ✅

get_contador() implementado

get_ultimo_saludo() implementado

Entiendes Option vs Result

Compila sin errores

# 🧑‍💼 FASE 6: Función administrativa

💡 Recordatorio:
El operador ? indica “si todo está bien, continúa; si no, detente”.

### Checkpoint 6 ✅

reset_contador() implementado

Verifica admin

Control de acceso funcional

Compila sin errores

# 🧪 FASE 7: Pruebas

Depues de hacer la tarea de cero, probar los tests indivudualmente, lo logre!  
<img width="1033" height="281" alt="Screenshot 2025-10-26 173458" src="https://github.com/user-attachments/assets/dedcf6d4-cba3-4a47-8c3e-f4f6d7a56e96" />


### Checkpoint 7 
✅6 tests implementados
✅ Todos los tests pasan
✅ Entiendes cada test
✅ Casos exitosos y de error verificados


⭐ FASE 8: A penas logre solucionar los tests completo esta fase

<img width="945" height="401" alt="Screenshot 2025-10-26 173816" src="https://github.com/user-attachments/assets/38332e19-7c26-4e3a-b49d-1011b42c10df" />

WASM 

<img width="910" height="102" alt="Screenshot 2025-10-26 175439" src="https://github.com/user-attachments/assets/5e0c292e-b3c4-4d55-9964-b1ce34e3c225" />

Checkpoint 
✅Build exitoso
✅WASM generado
✅WASM optimizado
