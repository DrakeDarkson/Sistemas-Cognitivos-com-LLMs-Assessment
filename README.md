# IndustrIA-RAG: Assistente Cognitivo para Consulta Histórica sobre Industrialização e Formação da Economia Moderna, 1836–1936

## 1. Descrição do projeto

Este projeto desenvolve uma aplicação cognitiva com LLM e RAG para responder perguntas em linguagem natural sobre o processo de industrialização e a formação da economia moderna entre 1836 e 1936.

A aplicação utiliza uma base documental histórica, geração de embeddings, recuperação semântica de trechos relevantes e geração de respostas fundamentadas no contexto recuperado.

## 2. Objetivo

Permitir que um usuário faça perguntas históricas sobre industrialização, países, tecnologias, trabalho, imperialismo, crises econômicas e modelos de desenvolvimento, recebendo respostas estruturadas e baseadas em documentos do corpus.

Exemplos de perguntas que a aplicação busca responder:

```text
Quais países mais influenciaram a estrutura econômica moderna entre 1836 e 1936?
Como as ferrovias transformaram a economia industrial?
Qual foi o papel do Reino Unido na industrialização?
Como a crise de 1929 afetou o capitalismo industrial?
A União Soviética representou uma alternativa ao capitalismo industrial?
```

## 3. Corpus

O corpus do projeto é composto por documentos textuais sobre industrialização, economia moderna, países industrializados, tecnologias produtivas, trabalho urbano, imperialismo, Primeira Guerra Mundial, crise de 1929 e industrialização soviética.

Os documentos originais ficam armazenados em:

```text
data/raw/
```

Os arquivos processados, como chunks e representações intermediárias, ficam armazenados em:

```text
data/processed/
```

## 4. Estrutura do projeto

```text
data/raw/           Documentos originais do corpus
data/processed/     Chunks e arquivos processados
notebooks/          Notebooks Jupyter organizados por etapa
src/                Funções auxiliares do pipeline
outputs/            Resultados gerados, consultas e avaliações
report/             Relatório técnico em PDF
README.md           Instruções gerais do projeto
requirements.txt    Dependências necessárias
.gitignore          Arquivos ignorados pelo Git
```

## 5. Passos para execução

Crie e ative o ambiente Conda:

```bash
conda create -n industria-rag python=3.11 -y
conda activate industria-rag
```

Atualize o `pip` e instale as dependências:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Abra o Jupyter Lab:

```bash
jupyter lab
```

## 6. Ordem recomendada dos notebooks

Execute os notebooks na seguinte ordem:

```text
1. notebooks/c01_modelos_llm.ipynb
2. notebooks/c02_prompting.ipynb
3. notebooks/c03_embeddings_busca.ipynb
4. notebooks/c04_inferencia_local_ou_remota.ipynb
5. notebooks/c05_rag_pipeline.ipynb
```

## 7. Descrição dos notebooks

- `c01_modelos_llm.ipynb`: uso de modelos pré-treinados e tarefas NLP aplicadas ao domínio histórico.
- `c02_prompting.ipynb`: estratégias de prompt engineering, comparação de prompts e saída estruturada.
- `c03_embeddings_busca.ipynb`: geração de embeddings, busca vetorial e análise dos resultados recuperados.
- `c04_inferencia_local_ou_remota.ipynb`: estratégia de execução, privacidade, custo, latência e limitações.
- `c05_rag_pipeline.ipynb`: pipeline RAG completo, com recuperação de contexto e geração de respostas fundamentadas.

## 8. Saída esperada da aplicação

A aplicação deve gerar respostas estruturadas contendo, por exemplo:

```json
{
  "pergunta": "Quais países mais influenciaram a estrutura econômica moderna entre 1836 e 1936?",
  "resposta": "...",
  "atores_historicos": ["Reino Unido", "Estados Unidos", "Alemanha", "Japão", "União Soviética"],
  "fontes_recuperadas": ["..."],
  "nivel_confianca": "alto",
  "limitacoes": "..."
}
```