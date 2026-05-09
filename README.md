Paralegal Digital - Agente de IA com RAG
Status: Protótipo / Prova de Conceito (PoC)

O Paralegal Digital é uma solução de Inteligência Artificial generativa baseada numa arquitetura multi-agentes. Este sistema foi desenhado para automatizar a triagem documental e a redação de peças jurídicas. Através da ingestão de dados multimodais — transcrevendo áudios com Whisper, extraindo texto de imagens com EasyOCR e processando PDFs complexos — o agente orquestra modelos de linguagem quantizados (Qwen) para extrair teses jurídicas e injetar a redação final diretamente num ficheiro .docx formatado. O projeto integra capacidades de Retrieval-Augmented Generation (RAG) em tempo real para pesquisa de jurisprudência e apresenta uma interface interativa low-code construída em Streamlit para revisão humana (Human-in-the-loop).

## Arquitetura do Sistema

O fluxo de dados foi desenhado para simular o raciocínio jurídico através de uma pipeline de orquestração de múltiplos agentes:

1. **Ingestão Multimodal:** O sistema aceita a submissão de áudios, imagens e documentos de texto ou PDF. Utiliza algoritmos de transcrição e OCR para normalizar os dados brutos num corpus de texto único.
2. **Agente Investigador:** Analisa o corpus gerado, extrai um resumo cronológico dos factos e formula as teses jurídicas centrais (termos de pesquisa).
3. **RAG (Retrieval-Augmented Generation) & Agente Relator:** Os termos gerados são enviados para a Serper API para procurar jurisprudência real na web. O Agente Relator cruza então os factos do cliente com esta jurisprudência, gerando um relatório de viabilidade.
4. **Agente Redator:** Com base no relatório de triagem, este agente redige as secções da petição inicial (Factos, Direito, Tutela e Pedidos), injetando o texto final de forma automatizada num ficheiro `.docx` padronizado.

## Stack Tecnológico

A escolha das ferramentas reflete a prioridade pela **eficiência computacional**, correndo modelos locais de código aberto de forma otimizada:

* **Modelos & IA Generativa:** `transformers` da Hugging Face, utilizando o modelo local `Qwen/Qwen2.5-7B-Instruct`.
* **Otimização de Hardware:** Aplicação de quantização em 8-bits com `BitsAndBytes` para gestão eficiente da VRAM e `torch` para manipulação de tensores.
* **Processamento Multimodal:** `openai-whisper` (áudio), `EasyOCR` (visão computacional/imagens) e `PyMuPDF` (extração de PDFs).
* **Pesquisa Externa (RAG):** Integração com `Serper API` e `duckduckgo-search`.
* **Interface Low-code:** Prototipagem da interface de validação humana (Human-in-the-loop) desenvolvida integralmente em `Streamlit`.

* ## Como Executar

Para executar este projeto localmente, você necessitará de uma GPU compatível com CUDA.

1. Clone o repositório:
bash
git clone [https://github.com/Bernardo8408/paralegal-digital-agent.git](https://github.com/Bernardo8408/paralegal-digital-agent.git)

2.  Instale as dependências:
bash
pip install -r requirements.txt

3. Configure as suas chaves de API como variáveis de ambiente (SERPER_API, HF_TOKEN).

4. Inicie a aplicação Streamlit:
bash
streamlit run app_piloto.py

Próximos Passos (Roadmap)
[ ] Implementação de banco de dados vetorial (ChromaDB) para pesquisa de jurisprudência interna.

[ ] Refinamento do parseamento de PDFs complexos.

[ ] Integração nativa com LangChain/LangGraph para orquestração declarativa dos agentes.
