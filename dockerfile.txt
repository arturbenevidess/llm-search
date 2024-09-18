# 1. Usar uma imagem oficial do Python como base (Python 3.9)
FROM python:3.9-slim

# 2. Definir o diretório de trabalho dentro do contêiner
WORKDIR /app

# 3. Copiar o arquivo de dependências (requirements.txt) para o contêiner
COPY requirements.txt .

# 4. Instalar as dependências listadas no requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# 5. Copiar o restante do código da aplicação para o contêiner
COPY . .

# 6. Expor a porta 5000 (ou qualquer outra porta que o FastAPI use)
EXPOSE 5000

# 7. Definir variáveis de ambiente (substitua pelos seus valores reais)
ENV DISCOVERY_ENDPOINT=https://api.au-syd.discovery.watson.cloud.ibm.com/instances/3f96bdcb-8fc6-4a25-9ebb-d0cb07858268
ENV DISCOVERY_API_KEY=VXmiS4l02ukI5HTF8KxunQNJW8-ZsfFXmUY8P2fjj5ms
ENV PROJECT_ID=360b5d33-b4a2-4f19-af8b-be744d65d8c9
ENV COLLECTION_ID=2f2b96aa-4fa7-1e18-0000-0191bd1b9ac7
ENV LLAMA_API_ENDPOINT=163.109.84.89:11434

# 8. Comando para iniciar o aplicativo FastAPI com Uvicorn
CMD ["uvicorn", "src.index:app", "--host", "0.0.0.0", "--port", "5000"]
