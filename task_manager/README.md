# ⬡ Orkestia — Sistema de Gestión de Tareas Empresarial

**Orquesta tu operación con Inteligencia**

Desarrollado por **Daniel Suarez**
Python para IA — Maestría en Inteligencia Artificial
Universidad de La Salle

---

## 🚀 Instalación y Ejecución

### Requisitos
- Python 3.9 o superior
- pip (incluido con Python)

### Pasos

```bash
# 1. Abre una terminal en la carpeta task_manager/

# 2. Instala las dependencias
pip install -r requirements.txt

# 3. Ejecuta la aplicación
python main.py
```

> **Nota:** Asegúrate de que `logo.png` esté en la misma carpeta que `main.py`.
> La primera ejecución descarga automáticamente la fuente Poppins de Google Fonts.

---

## 📁 Estructura del Proyecto

```
task_manager/
├── main.py              ← Código principal (todo en un archivo)
├── logo.png             ← Logo de Orkestia
├── requirements.txt     ← Dependencias PIP
├── README.md            ← Este archivo
├── fonts/               ← Fuente Poppins (auto-descargada)
├── data/
│   ├── tareas.txt       ← Datos en formato JSON (archivo de texto)
│   ├── tareas.pkl       ← Datos en formato pickle (archivo binario)
│   └── avatars/         ← Fotos de perfil de usuarios
├── reportes/            ← Informes exportados (TXT y XLSX)
└── backups/             ← Copias de seguridad (.pkl)
```

---

## 🖥️ Funcionalidades por Módulo

### 📊 Dashboard
- 6 tarjetas con estadísticas en tiempo real (total, pendientes, en progreso, completadas, vencidas, usuarios)
- Gráfico de barras apiladas: distribución de tareas por usuario (pendiente/progreso/completada)
- Diagrama de torta: distribución porcentual de estados
- Resumen de usuarios con avatar y cantidad de tareas asignadas

### 📋 Gestión de Tareas
- Tabla con columnas: Actividad, Responsable, Prioridad, Fecha Creación, Vencimiento, Estado, SLA/Plazo
- **SLA Heatmap**: Barra de calor con días restantes — verde (7+), amarillo (4-6), rojo (0-3), rojo oscuro (vencida)
- Filtros con etiquetas: Estado, Usuario, Vencimiento hasta (con calendario popup), Búsqueda
- Botón "Siguiente Estado ▸" para avance rápido del flujo
- Fecha de creación automática (no editable)
- Selección de fecha con **Calendar Popup** (Toplevel independiente, funcional en Mac/Windows/Linux)

### 👥 Gestión de Usuarios
- CRUD completo con foto de perfil (avatar circular con Pillow)
- Iniciales automáticas si no hay foto
- Estadísticas: total, activas, completadas por usuario
- Protección: no se puede eliminar un usuario con tareas activas

### 📈 Informes
- Vista previa del informe en formato texto
- **Exportar TXT** — Informe legible con tabulate
- **Crear Backup** — Archivo binario pickle con timestamp
- **Descargar Excel** — Archivo .xlsx con dos hojas (Tareas y Usuarios), headers violeta, formato profesional

### 🎨 Interfaz
- Tema claro estilo Monday.com con paleta violeta/blanco
- Fuente Poppins (descarga automática)
- Sidebar colapsable con animación suave (250px ↔ 68px)
- Tooltips en todos los botones e interacciones
- Logo grande (120px) del director de orquesta

---

## 🎯 Temas del Caso de Estudio Aplicados

### 1. Paquetes y PIP
| Paquete | Uso |
|---------|-----|
| `customtkinter` | Interfaz gráfica moderna (tema claro) |
| `tabulate` | Tablas formateadas en informes |
| `tkcalendar` | Widget Calendar para selección de fechas |
| `openpyxl` | Generación de archivos Excel (.xlsx) |
| `Pillow` | Procesamiento de imágenes (avatares circulares) |

### 2. Cadenas y Métodos de Listas
- `str.strip()`, `str.title()`, `str.lower()`, `str.split()`, `str.join()` — normalización de datos
- `list.append()`, `list.copy()`, `list.sort(key=lambda)` — gestión de colecciones
- List comprehensions — filtrado y transformación de datos
- `filter()`, `lambda`, `any()`, `next()` — operaciones funcionales sobre listas

### 3. Programación Orientada a Objetos (POO)
- **Clase `Usuario`** — atributos, serialización, `@classmethod from_dict`
- **Clase `Tarea`** — constantes de clase (`ESTADOS`, `PRIORIDADES`), métodos (`cambiar_estado`, `modificar`, `dias_restantes`, `porcentaje_sla`, `siguiente_estado`), encapsulamiento (`_log`)
- **Clase `GestorTareas`** — lógica central, generadores, manejo de archivos
- **Clase `App(ctk.CTk)`** — herencia, interfaz gráfica completa
- **Clase `Tooltip`** — widget auxiliar con eventos bind
- **Clase `CalendarPopup`** — ventana emergente reutilizable

### 4. Manejo de Archivos
- **Archivos de texto**: JSON con `json.dump()` / `json.load()` (codificación UTF-8)
- **Archivos binarios**: pickle con `pickle.dump()` / `pickle.load()` para serialización completa
- **Backups**: archivos binarios con timestamp automático
- **Informes TXT**: exportación con tabulate
- **Informes XLSX**: exportación con openpyxl (headers, estilos, múltiples hojas)
- **Imágenes**: lectura, recorte circular, almacenamiento en carpeta avatars/

### 5. Módulos Misceláneos
| Módulo | Uso |
|--------|-----|
| `os` | `os.makedirs()`, `os.path.exists()` — estructura de directorios |
| `datetime` | Cálculo de días restantes, plazos, SLA, timestamps, formateo de fechas |
| `calendar` | Calendario mensual en informes de texto |
| `time` | Disponible para mediciones |
| `uuid` | Generación de IDs únicos para tareas y usuarios |
| `pathlib` | Manejo moderno de rutas de archivos |
| `shutil` | Copia de archivos (avatares, fuentes) |
| `platform` | Detección de SO para registro de fuentes |
| `math` | Cálculos para dibujo de gráficos (torta) |
| `ctypes` | Registro de fuentes en Windows (GDI API) |

### 6. Generadores e Iteradores
- `gen_por_estado(estado)` — `yield` tareas filtradas por estado
- `gen_por_usuario(uid)` — `yield` tareas por responsable
- `gen_vencidas()` — `yield` tareas expiradas

---

## 📝 Notas Técnicas

- **Persistencia dual**: Los datos se guardan simultáneamente en JSON (legible) y pickle (binario). Al cargar, se prioriza el binario por velocidad, con fallback al JSON.
- **Calendario Popup**: Se usa un `tk.Toplevel` independiente con el widget `Calendar` de tkcalendar. Esto evita los problemas de rendering que ocurren al embeber `DateEntry` dentro de frames scrollables de CustomTkinter, especialmente en macOS.
- **SLA Heatmap**: La barra calcula el porcentaje de avance del plazo y colorea según los días restantes, no según el porcentaje, para mayor utilidad visual.
- **Fuentes**: Poppins se descarga una sola vez y se registra nativamente en el SO (Windows: GDI, macOS: ~/Library/Fonts, Linux: ~/.local/share/fonts).
