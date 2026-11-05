from fastapi import FastAPI
from pydantic import BaseModel
# Importa aqui a biblioteca da API da IA que vais usar (ex: google.generativeai)

app = FastAPI(title="Matific Helper")

class DadosPagina(BaseModel):
    conteudo: str

@app.get("/") 
def home(): 
    return { "status": "online", "project": "Matific Helper" }

@app.get("/health") 
def health(): 
    return { "status": "ok" }

@app.post("/processar")
def processar_pagina(dados: DadosPagina):
    texto_pagina = dados.conteudo
    
    # === COLOCAS A TUA API AQUI ===
    # 1. Autenticas com a tua chave de API
    # 2. Envias o 'texto_pagina' como prompt para a IA pedir a resposta correta
    # 3. Guardas o resultado numa variável, por exemplo: resposta_ia
    
    # Exemplo simulado:
    resposta_ia = "Aqui virá a resposta calculada pela IA com base no texto da página."
    
    return {
        "status": "sucesso",
        "resposta": resposta_ia
    }

  
