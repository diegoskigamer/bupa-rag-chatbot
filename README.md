# 🏥 Chatbot RAG — Bupa Chile
### ISY0101 Ingeniería de Soluciones con IA — Evaluación Parcial N°1

Agente conversacional inteligente para atención al paciente de Bupa Chile, implementado con LLM + pipeline RAG. Responde consultas frecuentes sobre coberturas, reembolsos, horarios y protocolos médicos, con trazabilidad documental y escalada automática ante urgencias.

---

## 🗂️ Estructura del repositorio

```
📁 bupa-rag-chatbot/
├── Bupa_Chile_RAG_FINAL.ipynb   ← Notebook principal (ejecutar en Colab)
├── README.md                    ← Este archivo
└── docs/
    └── arquitectura.png         ← Diagrama de arquitectura del sistema
```

---

## ⚙️ Stack tecnológico

| Componente | Tecnología | Costo |
|---|---|---|
| LLM | google/flan-t5-large 
| Embeddings | paraphrase-multilingual-MiniLM-L12-v2 
| Vector Store | ChromaDB 
| Framework | LangChain (LCEL) 
| Infraestructura | Google Colab (GPU T4) 

---

## 🚀 Instrucciones de ejecución



| Celda | Descripción | Tiempo estimado |
|---|---|---|
| Paso 1 | Instalación de dependencias | ~2 min |
| Paso 2 | Carga de documentos Bupa | ~5 seg |
| Paso 3 | Embeddings + ChromaDB | ~1 min |
| Paso 4 | Carga del LLM Flan-T5 | ~2 min |
| Paso 5 | Pipeline RAG (LCEL) | ~5 seg |
| Paso 6 | Función de consulta | ~5 seg |
| Paso 7 | Pruebas automáticas | ~1 min |
| Paso 8 | Chat interactivo | indefinido |



### Opción B — Ejecución local

```bash
# Clonar repositorio
git clone https://github.com/tu-usuario/bupa-rag-chatbot.git
cd bupa-rag-chatbot

# Instalar dependencias
pip install langchain langchain-community langchain-chroma langchain-huggingface \
            langchain-core langchain-text-splitters chromadb sentence-transformers \
            transformers torch accelerate jupyter

```

---

## 💬 Uso del chatbot

Una vez ejecutadas todas las celdas, usa la función `consultar_bupa()`:

```python
# Consulta sobre coberturas
consultar_bupa("¿Qué cubre el plan Bupa Esencial para especialistas?")

# Consulta sobre reembolsos
consultar_bupa("¿Cómo pido un reembolso?")

# Consulta sobre horarios
consultar_bupa("¿Cuáles son los horarios del centro de Las Condes?")

# Chat interactivo (Paso 8)
# Escribe cualquier pregunta cuando aparezca: "Tu consulta:"
# Escribe "salir" para terminar
```

---

## 🧪 Pruebas incluidas

1. ✅ Consulta de coberturas plan Esencial
2. ✅ Proceso de reembolso
3. ✅ Agendamiento de horas médicas
4. ✅ Horarios centros médicos
5. ✅ Protocolo de ayuno para exámenes
6. ✅ Detección de urgencia médica (derivación automática sin LLM)
7. ✅ Telemedicina fin de semana

---

## 🏗️ Arquitectura del sistema

```
Usuario
   │
   ▼
[FastAPI] ──► Clasificador urgencia ──► ⚠️ Derivación 131
   │
   ▼
[Retriever ChromaDB]
   │  Top-3 fragmentos por similitud coseno
   ▼
[Flan-T5 LLM] ◄── Contexto documental + Pregunta
   │
   ▼
Respuesta + Fuente documental
   │
   ▼
[Salesforce CRM] + [Audit Log]
```

Ver diagrama completo en `docs/arquitectura.png`

---

## 📁 Base de conocimiento (documentos simulados)

| Documento | Categoría |
|---|---|
| Cartilla_Coberturas_Esencial_2024.pdf | Coberturas |
| Cartilla_Coberturas_Premium_2024.pdf | Coberturas |
| Reglamento_Reembolsos_2024.pdf | Reembolsos |
| Directorio_Centros_RM_2024.pdf | Horarios |
| Guia_Agendamiento_2024.pdf | Agendamiento |
| Protocolo_Examenes_Laboratorio.pdf | Protocolos clínicos |
| Guia_Telemedicina_2024.pdf | Telemedicina |

---

## ⚠️ Restricciones implementadas

- El chatbot **no emite diagnósticos médicos**
- Ante palabras de urgencia (`dolor pecho`, `emergencia`, etc.) deriva automáticamente al **131** sin llamar al LLM
- Todas las respuestas incluyen la **fuente documental** (trazabilidad)
- Cumple con principios de la **Ley 19.628** de protección de datos

---

## 📚 Referencias

- Chase, H. (2022). *LangChain* [Software]. https://github.com/langchain-ai/langchain
- Reimers, N., & Gurevych, I. (2019). Sentence-BERT. *EMNLP 2019*. https://arxiv.org/abs/1908.10084
- Lewis, P., et al. (2020). RAG for Knowledge-Intensive NLP Tasks. *NeurIPS 2020*. https://arxiv.org/abs/2005.11401
- Chroma. (2024). *ChromaDB documentation*. https://docs.trychroma.com

---
