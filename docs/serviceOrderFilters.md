➡️ [Volver a la documentación principal](../README.md)

# ✨ Condiciones y Filtros – Órdenes de Servicio

Este documento explica la **lógica de negocio** utilizada por la automatización para clasificar proyectos y aplicar filtros de fechas.  


---

## 📅 1) Filtro de Fechas

El sistema ajusta automáticamente el período de consulta de las órdenes de servicio según el **día del mes** en que se ejecute:

1. 🗓️ **Primera semana del mes (días 1 al 7):**  
   ➡️ Se seleccionan registros **desde el 1º del mes hasta el día siguiente al actual**.  
   > Ejemplo: si hoy es **5 de marzo**, se toman datos del **1 al 6 de marzo**.

2. 📊 **Primera mitad del mes (días 8 al 14):**  
   ➡️ Se seleccionan registros **desde el 1º del mes hasta el día actual**.  
   > Ejemplo: si hoy es **10 de marzo**, se toman datos del **1 al 10 de marzo**.

3. 📆 **Segunda mitad del mes (día 15 en adelante):**  
   ➡️ Se consultan los registros del **mes completo** (desde el 1º hasta el último día del mes).  
   > Ejemplo: si hoy es **20 de marzo**, se toman datos del **1 al 31 de marzo**.

---

## 🏗️ 2) Condiciones para determinar el estado de un proyecto

El proyecto puede clasificarse en tres estados principales:

- ✅ **Proyecto Finalizado**  
- ⚡ **Finalizado por Directriz**  
- 🔄 **En Ejecución (por defecto)**

La decisión sigue un **orden de prioridad**, evaluando cada regla hasta encontrar la primera que aplique.

---

### ✅ 2.1 Proyecto Finalizado
- **Criterio:** Todas las visitas programadas fueron realizadas.  
- **Interpretación:** Avance = **100%**.  
- **Resultado:** El proyecto se marca como **PROYECTO FINALIZADO**.

---

### ⚡ 2.2 Finalizado por Directriz
Un proyecto puede cerrarse por directriz en cualquiera de los siguientes casos:

1. 📈 **Avance ≥ 65%**  
   - Aunque no esté finalizado, se considera suficientemente avanzado.

2. 🔢 **2 visitas programadas y solo 1 realizada**  
   - Caso especial que se da por concluido.

3. 💰 **Proyectos de bajo valor (< 5 millones)** con **al menos 1 visita realizada**  
   - Para proyectos pequeños no se exige completar todas las visitas.

- **Resultado:** El proyecto se marca como **FINALIZADO POR DIRECTRIZ**.

---

### 🔄 2.3 En Ejecución
- **Criterio:** Ninguna de las condiciones anteriores aplica.  
- **Interpretación:** El proyecto sigue en curso.  
- **Resultado:** Estado **EN EJECUCIÓN**.
---

