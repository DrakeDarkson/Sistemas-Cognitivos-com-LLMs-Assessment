# historIA-RAG: Assistente Cognitivo para Consulta Histórica

Projeto desenvolvido para o assessment da disciplina **Sistemas Cognitivos com LLMs**.

## 1. Descrição do projeto

O **historIA-RAG** é uma aplicação cognitiva funcional em Python, organizada em notebooks Jupyter Lab e executada em ambiente Anaconda.

A aplicação recebe perguntas em linguagem natural sobre um período histórico, recupera trechos relevantes de uma base documental própria e gera respostas estruturadas com apoio de um modelo de linguagem.

O projeto se enquadra principalmente como um **sistema de perguntas e respostas com base em corpus próprio**, associado a uma **busca semântica em base de conhecimento**. Também incorpora elementos de extração estruturada de informações, pois as respostas são organizadas em formato controlado, com campos como pergunta, resposta, atores históricos, fontes recuperadas, nível de confiança e limitações.

## 2. Problema escolhido

O problema que este projeto busca solucionar é a dificuldade de consultar, cruzar e sintetizar informações históricas sobre um determinado período da história de forma rápida e eficaz, sem exigir especialização acadêmica prévia nem o esforço de consultar dezenas de documentos, livros e fontes distintas para obter um contexto inicial sobre determinados acontecimentos históricos.

O corpus utilizado retrata um século de transformações, mais especificamente o período de **1836 a 1936**, marcado por mudanças econômicas, tecnológicas, sociais e políticas. Entre esses processos estão a expansão ferroviária, a transição energética associada ao carvão e ao petróleo, o uso crescente do aço, a eletrificação, a urbanização, o trabalho assalariado, o imperialismo, o capitalismo industrial, a Primeira Guerra Mundial, a crise de 1929 e a industrialização soviética.

Como essas informações geralmente aparecem separadas por país, evento, tecnologia ou processo histórico, perguntas amplas e comparativas exigem recuperação e combinação de múltiplos trechos documentais.

Exemplos de perguntas que a aplicação busca responder:

```text
Quais países mais influenciaram a estrutura econômica moderna?
Como as ferrovias transformaram a economia industrial?
Qual foi o papel do Reino Unido na industrialização?
Como a crise de 1929 afetou o capitalismo industrial?
A União Soviética realmente representou uma alternativa ao capitalismo industrial?
```

## 3. Objetivo da aplicação

O objetivo principal da aplicação é auxiliar estudantes, professores, entusiastas e demais usuários interessados em história a consultar, relacionar e sintetizar informações sobre a industrialização e a formação da economia moderna no período analisado.

A proposta não é apenas retornar documentos relacionados à pergunta, mas recuperar trechos relevantes do corpus, utilizar esses trechos como contexto para um modelo de linguagem e gerar uma resposta estruturada, fundamentada e acompanhada de limitações quando a base documental não possuir informação suficiente.

A aplicação deve ser capaz de:

- Receber perguntas abertas sobre o período histórico de 1836 a 1936.
- Identificar documentos e trechos semanticamente relacionados à pergunta.
- Recuperar os trechos mais relevantes por meio de embeddings e busca vetorial.
- Utilizar o contexto recuperado para orientar a resposta do modelo de linguagem.
- Gerar uma saída estruturada com fontes recuperadas, atores históricos citados, nível de confiança e limitações da resposta.
- Indicar quando o corpus não possui informação suficiente para responder com segurança.

## 4. Corpus

O corpus do projeto é composto por documentos textuais autorais e sintéticos, criados para simular uma base de conhecimento histórica sobre industrialização e formação da economia moderna entre 1836 e 1936.

A escolha por um corpus próprio e controlado tem três finalidades principais:

1. garantir reprodutibilidade, permitindo que todos os documentos utilizados estejam disponíveis no repositório;
2. evitar a inclusão direta de textos protegidos por direitos autorais, já que os documentos foram redigidos em linguagem autoral a partir de pesquisa e paráfrase de fontes confiáveis;
3. permitir cobertura equilibrada dos temas necessários para testar busca semântica, recuperação de contexto, comparação entre respostas e pipeline RAG.

Os documentos originais ficam armazenados em:

```text
data/raw/
```

Arquivos do corpus:

```text
01_contexto_geral_1836_1936.txt
02_reino_unido_primeira_industrializacao.txt
03_ferrovias_carvao_aco.txt
04_segunda_revolucao_industrial.txt
05_estados_unidos_capitalismo_industrial.txt
06_alemanha_industria_ciencia_estado.txt
07_japao_modernizacao_meiji.txt
08_imperialismo_materias_primas.txt
09_trabalho_urbano_movimentos_operarios.txt
10_primeira_guerra_economia_industrial.txt
11_crise_1929_capitalismo.txt
12_urss_planejamento_industrializacao.txt
```

Os arquivos processados, como chunks, representações intermediárias e resultados derivados, ficam armazenados em:

```text
data/processed/
```

## 5. Visão geral da arquitetura

A arquitetura geral da aplicação segue o fluxo abaixo:

1. carregamento dos documentos do corpus;
2. divisão dos textos em chunks;
3. geração de embeddings para cada chunk;
4. indexação dos embeddings em mecanismo de busca vetorial;
5. recebimento de pergunta em linguagem natural;
6. geração de embedding da pergunta;
7. recuperação dos trechos mais relevantes;
8. construção de prompt aumentado com contexto;
9. geração de resposta pelo modelo de linguagem;
10. validação ou interpretação da saída estruturada;
11. apresentação da resposta com fontes, confiança e limitações.

## 6. Estrutura do projeto

```text
data/processed/     Chunks e arquivos processados
data/raw/           Documentos originais do corpus
notebooks/          Notebooks Jupyter organizados por etapa
outputs/            Resultados gerados, consultas e avaliações
.gitignore          Arquivos ignorados pelo Git
README.md           Instruções gerais do projeto
requirements.txt    Dependências necessárias
```

## 7. Passos para execução

Crie e ative o ambiente Conda:

```bash
conda create -n historia-rag python=3.11 -y
conda activate historia-rag
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

## 8. Ordem recomendada dos notebooks

Execute os notebooks na seguinte ordem:

```text
1. notebooks/c01_modelos_llm.ipynb
2. notebooks/c02_prompting.ipynb
3. notebooks/c03_embeddings_busca.ipynb
4. notebooks/c04_inferencia_local_ou_remota.ipynb
5. notebooks/c05_rag_pipeline.ipynb
```

## 9. Descrição dos notebooks

- `c01_modelos_llm.ipynb`: uso de modelos pré-treinados e tarefas NLP aplicadas ao domínio histórico.
- `c02_prompting.ipynb`: estratégias de prompt engineering, comparação de prompts e saída estruturada.
- `c03_embeddings_busca.ipynb`: geração de embeddings, busca vetorial e análise dos resultados recuperados.
- `c04_inferencia_local_ou_remota.ipynb`: estratégia de execução, privacidade, custo, latência e limitações.
- `c05_rag_pipeline.ipynb`: pipeline RAG completo, com recuperação de contexto e geração de respostas fundamentadas.

## 10. Saída esperada da aplicação

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