# Firat-frontend
Microservice that represent graphically the daily news
Architecture
[ RSS Sources ]
       |
       v
[ Ingestion Service ]
       |
       v
[ Backend API ]
       |
       v
[ Event Trigger ]
       |
       v
[ AI Agent Service ]
       |
       v
[ Storage / Insights ]
       |
       v
[ Frontend ]

Ahora vamos bloque por bloque 👇

1️⃣ RSS Sources

Fuentes externas:

periódicos

blogs

feeds

🔹 No tienen lógica
🔹 Solo datos crudos

2️⃣ Ingestion Service (Docker)

Este es CLAVE y mucha gente se lo salta.

Puede ser:

un cron interno

un worker

un job

Cada X minutos
→ fetch RSS
→ normaliza
→ envía al backend


📌 Evento: tiempo

En draw.io:
🕒 ícono de reloj

3️⃣ Backend API (tu backend actual)

Responsabilidades:

validar datos

deduplicar

guardar estado

exponer endpoints

📌 Aquí ocurre el EVENTO REAL:

if (new_articles_detected) {
  emit EVENT
}


En draw.io:
⚡ o 🔔

4️⃣ Event Trigger (conceptual, no siempre código)

Esto puede ser:

una función

un mensaje

una cola

un flag

Ejemplo lógico:

"NEWS_UPDATED"


📌 Es el puente entre backend e IA

5️⃣ AI Agent Service (Docker separado)

🚨 IMPORTANTE: IA en su propio contenedor

Este servicio:

NO escucha usuarios

NO tiene UI

SOLO reacciona a eventos

Flujo:

EVENT
→ fetch context from backend
→ analyze
→ generate insights
→ store results


En draw.io:
🤖

6️⃣ Storage / Insights

Puede ser:

DB normal

vector DB

JSON

cache

Aquí se guardan:

resúmenes

scores

embeddings

etiquetas

📌 La IA no habla con el frontend

7️⃣ Frontend

Solo consume:

GET /news
GET /analysis


Nunca:

llama a la IA

dispara procesos

Cómo se activa SIN que tú hagas nada

Este es el loop automático:

Docker up
→ scheduler corre
→ RSS cambia
→ backend detecta
→ EVENT
→ IA se activa
→ resultados guardados
→ frontend muestra


Tú mientras:
☕ trabajando
🎧 música
🧠 foco

¿Cómo lo dibujas en draw.io? (tips rápidos)

Rectángulos = servicios

Cilindro = storage

Rayo ⚡ = evento

Flechas sólidas = datos

Flechas punteadas = control

Ponle títulos tipo:

“Event-driven trigger”

“Autonomous AI Agent”

“Single source of truth”

Frase que define tu sistema

Guárdala porque es CV-level:

“An event-driven, autonomous AI agent architecture for continuous news analysis.”

Siguiente nivel (opcional)

Si quieres hacerlo aún más sexy:

message queue (Redis / RabbitMQ)

retries

backoff

observabilidad

Si quieres, en el próximo mensaje puedo:

ayudarte a nombrar cada bloque exactamente

darte un layout perfecto para draw.io

o ayudarte a justificar esta arquitectura en una entrevista

Dime por dónde seguimos 😎🤖
