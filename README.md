# 🧵 bluepill-baremetal :)

🎯 **Proyecto minimalista para programar la Blue Pill (STM32F103C8T6) en bare-metal usando WSL2.**  
Sin HAL, sin magia: solo registros, C puro y un Makefile simple. Ideal para aprender cómo funciona todo desde adentro 🔍⚙️

---
> ⚠️ Este entorno fue probado en WSL2 (Ubuntu), pero también es compatible con cualquier distribución Linux que tenga las herramientas instaladas.

---

## 📦 Estructura del proyecto

```
bluepill-baremetal/
├── src/               # Código fuente en C (sin HAL)
├── bin/               # Binarios generados (.elf, .bin, .map)
├── obj/               # Archivos objeto intermedios
├── docs/              # Documentación técnica del proyecto
│   ├── main.md        # Análisis detallado del main.c
│   ├── startup.md     # Explicación del startup.c
│   ├── linker.md      # Explicación del script de linker
│   └── toolchain.md   # Explicación del entorno de desarrollo
├── linker.ld          # Script de linker personalizado
├── Makefile           # Build system simple y transparente
└── README.md          # Este archivo ✍️

```

---

## 🚀 Cómo compilar y flashear

Este proyecto está pensado para usarse con **WSL2 + arm-none-eabi-gcc + OpenOCD**.

### 🔧 Requisitos

- [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install)
- Toolchain ARM:
  ```bash
  sudo apt install gcc-arm-none-eabi
  ```
- OpenOCD:
  ```bash
  sudo apt install openocd
  ```
- ST-Link conectado por USB

### 🔨 Compilar

```bash
make
```

Esto genera:

- `bin/blink_minimal.elf`: binario ELF con info de depuración 🧠
- `bin/blink_minimal.bin`: binario puro para flashear 🚀
- `bin/blink_minimal.map`: mapa de memoria 📊

### ⚡ Flashear la placa

```bash
make flash
```

> Usa OpenOCD con configuración para ST-Link y STM32F1.

### 🐛 Debug con GDB

1. En una terminal:
   ```bash
   make openocd
   ```

2. En otra:
   ```bash
   make gdb
   ```

---

## 🧰 Uso con VS Code (.vscode/)

Este repositorio incluye configuración lista para usar con **Visual Studio Code** como entorno de desarrollo embebido.

### 🧠 ¿Qué incluye?

- **`launch.json`**  
  Configuración para depurar con la extensión [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug).  
  Permite debuggear con `F5`, detenerse en `main()`, ver registros, memoria y periféricos.

- **`tasks.json`**  
  Define tareas automáticas:
  - `Ctrl+Shift+B` → compila (`make`)
  - `Ctrl+Shift+P → Run Task → clean` → limpia (`make clean`)
  - `Ctrl+Shift+P → Run Task → flash` → flashea (`make flash`)

### ⚙️ Requisitos

- [Visual Studio Code](https://code.visualstudio.com/)
- Extensión [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)
- Herramientas instaladas:
  - `make`
  - `arm-none-eabi-gcc`
  - `openocd`

### 🧪 Flujo sugerido con VS Code

1. Abrí el proyecto en VS Code
2. Presioná `Ctrl+Shift+B` para compilar
3. Presioná `F5` para iniciar la depuración (requiere ST-Link conectado)
4. Usá `Run Task` (`Ctrl+Shift+P`) para acceder a `clean` o `flash` si lo deseás

---


## 🎓 Ideal para...

- Estudiantes de sistemas embebidos
- Docentes que quieren enseñar desde lo más bajo nivel
- Curiosos del hardware que prefieren saber **exactamente qué está pasando**

---

## 📚 Expansiones sugeridas

- Agregar manejo de interrupciones 🧠
- Controlar periféricos como GPIO, USART, ADC, etc. 💡
- Agregar FreeRTOS desde cero 🧵

---

## 🧠

> “No se puede controlar lo que no se comprende.”  
> — Richard Feynman, probablemente

---

## 🪪 Licencia

Este proyecto está licenciado bajo los términos de la [Licencia MIT](LICENSE).

---

## 📘 Documentación técnica

> ¿Querés entender cómo funciona todo por dentro? Explorá los siguientes archivos:

- [main.md](docs/main.md): explicación detallada del programa de ejemplo (blink).
- [startup.md](docs/startup.md): cómo arranca el sistema desde el reset.
- [linker.md](docs/linker.md): cómo se organiza la memoria con el linker script.
- [toolchain.md](docs/toolchain.md): recorrido completo por la toolchain y sus herramientas.

> Todos estos documentos están en la carpeta `docs/`.

