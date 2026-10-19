# 🐾 Mokepon

> **Mokepon** es un videojuego web 2D multijugador desarrollado como proyecto práctico del **Curso de Programación Básica de Platzi**. Los jugadores eligen su mascota Mokepon, exploran un mapa interactivo renderizado en HTML5 Canvas, detectan colisiones con otros jugadores en tiempo real y libran combates estratégicos por turnos basados en ventajas elementales.

### 🎓 Certificación y Diploma
- 📜 **Diploma Oficial en Platzi**: Puedes consultar la validación oficial en línea en el siguiente enlace: [Ver Diploma Oficial de Platzi](https://platzi.com/p/angelortegacorrea09/curso/3208-programacion-basica-2022/diploma/detalle/).
- 📁 **Certificado en Repositorio**: El archivo original en formato PDF se encuentra disponible para su visualización en la carpeta [`certificado/`](./certificado/).

---

## 🎮 Demostración y Flujo de Juego

1. **Selección de Mascota**: Escoge tu Mokepon preferido entre Hipodoge, Capipepo y Ratigueya.
2. **Exploración en el Mapa**: Muévete por el mapa interactivo utilizando los controles en pantalla o las flechas del teclado.
3. **Multijugador en Tiempo Real**: El servidor sincroniza la posición de todos los jugadores conectados en la misma red.
4. **Detección de Colisiones**: Acércate a otro Mokepon para iniciar automáticamente la batalla.
5. **Combate Elemental**: Selecciona tus 5 ataques y compite por la victoria basándote en debilidades y fortalezas elementales.

---

## ✨ Características Principales

- 🗺️ **Mapa en Canvas 2D**: Renderizado fluido a 20 FPS usando la API de Canvas 2D de HTML5.
- 🕹️ **Controles Duales**: Soporte tanto para controles en pantalla (clic / mouse down) como para controles por teclado (`ArrowUp`, `ArrowDown`, `ArrowLeft`, `ArrowRight`).
- 🌐 **Backend Multijugador (REST API)**: Arquitectura cliente-servidor construida con Node.js y Express para gestionar jugadores, sincronizar coordenadas y transmitir ataques.
- 💥 **Sistema de Combate por Turnos**: Lógica de combate inspirada en piedra, papel o tijera con 5 rondas dinámicas y conteo de victorias.
- 📱 **Diseño Responsivo**: Adaptado con CSS Grid y Flexbox para diferentes resoluciones de pantalla.

---

## 🐾 Mascotas y Elementos

| Mascota | Tipo Principal | Ataques | Ventaja |
| :---: | :---: | :---: | :---: |
| **Hipodoge** | 💧 Agua | 3x Agua 💧, 1x Fuego 🔥, 1x Tierra 🍃 | Fuerte contra Fuego 🔥 |
| **Capipepo** | 🍃 Tierra | 3x Tierra 🍃, 1x Agua 💧, 1x Fuego 🔥 | Fuerte contra Agua 💧 |
| **Ratigueya** | 🔥 Fuego | 3x Fuego 🔥, 1x Agua 💧, 1x Tierra 🍃 | Fuerte contra Tierra 🍃 |

### ⚔️ Reglas de Efectividad
- **Fuego (🔥)** vence a **Tierra (🍃)**
- **Agua (💧)** vence a **Fuego (🔥)**
- **Tierra (🍃)** vence a **Agua (💧)**
- Si ambos eligen el mismo elemento, la ronda resulta en **Empate**.

---

## 🛠️ Tecnologías Utilizadas

### Frontend
- **HTML5**: Estructura semántica y elemento `<canvas>` para gráficos 2D.
- **CSS3**: Flexbox, CSS Grid, media queries y Google Fonts (`Fredoka`, `Poppins`).
- **JavaScript (ES6+)**: POO (Clases), manejo del DOM, eventos de teclado y consumo de API con `fetch`.

### Backend
- **Node.js**: Entorno de ejecución en el servidor.
- **Express.js (v5)**: Enrutador HTTP para la API REST del juego.
- **CORS**: Middleware para habilitar el intercambio de recursos de origen cruzado.

---

## 🚀 Instalación y Puesta en Marcha

### Prerrequisitos
- Tener instalado [Node.js](https://nodejs.org/) (versión 16 o superior).
- Un navegador web moderno (Google Chrome, Firefox, Brave, Edge).

### Pasos

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/LuisOrCo/Mokepon.git
   cd Mokepon
   ```

2. **Instalar dependencias:**
   ```bash
   npm install
   ```

3. **Iniciar el servidor backend:**
   ```bash
   node index.js
   ```
   > El servidor quedará escuchando en el puerto `http://localhost:8080`.

4. **Abrir el cliente:**
   Abre el archivo `mokepon.html` en tu navegador web preferido (o con la extensión Live Server de VS Code).

> [!TIP]
> Para jugar en multijugador local con amigos en la misma red Wi-Fi, cambia `localhost` por la IP local de tu ordenador (por ejemplo `http://192.168.1.XX:8080`) en [`js/mokepon.js`](./js/mokepon.js) y abre el juego desde dos dispositivos distintos.

---

## 📡 Endpoints de la API (Backend)

| Método | Endpoint | Descripción | Body (JSON) |
| :--- | :--- | :--- | :--- |
| `GET` | `/unirse` | Registra a un nuevo jugador y devuelve un identificador único (`jugadorId`). | Ninguno |
| `POST` | `/mokepon/:jugadorId` | Asigna la mascota seleccionada al jugador. | `{ "mokepon": "Capipepo" }` |
| `POST` | `/mokepon/:jugadorId/posicion` | Actualiza la posición (X, Y) y devuelve los enemigos conectados en el mapa. | `{ "x": 100, "y": 80 }` |
| `POST` | `/mokepon/:jugadorId/ataques` | Registra la secuencia de los 5 ataques seleccionados por el jugador. | `{ "ataques": ["💧", "🔥", ...] }` |
| `GET` | `/mokepon/:jugadorId/ataques` | Consulta los ataques seleccionados por el oponente para resolver el combate. | Ninguno |

---

## 📁 Estructura del Proyecto

```text
mokepon/
├── assets/                  # Sprites, avatares y fondo del mapa
│   ├── capipepo.png
│   ├── hipodoge.png
│   ├── ratigueya.png
│   ├── mokemap.png
│   └── ...
├── certificado/             # Diploma y certificado oficial de Platzi (PDF)
├── js/
│   └── mokepon.js           # Lógica del cliente, canvas y peticiones fetch
├── index.js                 # Servidor backend con Express y endpoints REST
├── mokepon.html             # Estructura del juego (vistas y canvas)
├── styles.css               # Estilos globales, diseño de tarjetas y animaciones
├── package.json             # Configuración del proyecto y dependencias
└── README.md                # Documentación del proyecto
```

---

## 👤 Autor

Desarrollado con dedicación por **Luis Ortega** ([@LuisOrCo](https://github.com/LuisOrCo)) como parte del proyecto práctico del **Curso de Programación Básica de Platzi**.

🎓 **Diploma y Certificado**:
- [Validación del Diploma Oficial en Platzi](https://platzi.com/p/angelortegacorrea09/curso/3208-programacion-basica-2022/diploma/detalle/)
- Documento disponible en la carpeta local: [`certificado/`](./certificado/)
