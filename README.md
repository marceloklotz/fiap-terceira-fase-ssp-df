# 🏫👨‍💻 Tech Challenge - Pós Tech (8IADT) FIAP - Fase 3: Assistente virtual de atendimento médico


Este repositório contém o notebook [FIAP_Fase_3.ipynb](https://github.com/marceloklotz/fiap-terceira-fase-ssp-df), que apresenta o desenvolvimento de um protótipo de assistente virtual especializado em saúde da mulher, com foco em triagem clínica e apoio à decisão. O projeto integra as quatro tecnologias centrais da Fase 3: Fine-tuning com LoRA, RAG com FAISS, LangChain e LangGraph. O projeto seguiu uma metodologia dividida em etapas técnicas claras:

- **Preparação do Ambiente:** Configuração do Google Colab com a instalação otimizada de bibliotecas essenciais como LangChain, LangGraph, Transformers, PEFT e FAISS.
- **Base de Dados Híbrida:** Utilização de um dataset de aproximadamente 280 registros, combinando literatura biomédica real filtrada do PubMedQA (em inglês) com dados sintéticos em português baseados em diretrizes da FEBRASGO, INCA e Ministério da Saúde.
- **Ajuste Fino (Fine-tuning) com LoRA:** Aplicação da técnica Low-Rank Adaptation (LoRA) para especializar o modelo base GPT-2 no domínio de saúde feminina, otimizando o treinamento para execução eficiente em ambientes de recursos limitados.
- **Implementação de RAG (Retrieval-Augmented Generation):** Integração do modelo a uma base de conhecimento vetorial contendo 6 protocolos clínicos detalhados (incluindo triagem, violência doméstica e pré-natal) através da biblioteca FAISS para busca semântica em milissegundos.
- **Orquestração com LangGraph:** Criação de quatro grafos de estados para gerenciar fluxos complexos de triagem: Ginecológica, Violência Doméstica, Obstétrica e Prevenção/Acompanhamento (este último utilizando arestas condicionais).
- **Avaliação Quantitativa e Ética:** Implementação de métricas rigorosas de desempenho, incluindo ROUGE-1/2/L para qualidade textual, cobertura de termos médicos para especialização de domínio e análise de bias e equidade demográfica para garantir tratamentos equânimes entre diferentes perfis de pacientes.

Link do notebook encontra-se disponível em:
https://github.com/marceloklotz/fiap-terceira-fase-ssp-df/

## 📝 Descrição do Desafio

A proposta do desafio foi desenvolver um assistente virtual médico personalizado, treinado com dados próprios da instituição, capaz de apoiar condutas clínicas, responder dúvidas de profissionais e sugerir procedimentos alinhados aos protocolos internos de atendimento feminino. O desafio também envolve a criação de fluxos automatizados, seguros e integrados, utilizando LangChain, para coordenar ações como verificação de exames ginecológicos pendentes, recomendação de tratamentos reprodutivos, emissão de alertas para possíveis casos de violência doméstica e articulação de atendimento multidisciplinar, considerando as particularidades e sensibilidades do cuidado à mulher.

Para tanto, utilizou-se o fine-tuning de LLMs com dados específicos da área e implementando fluxos automatizados de decisão clínica através do LangChain, sempre respeitando protocolos de segurança, privacidade e sensibilidade cultural específicos do atendimento feminino, conforme instruções da disciplina da Pós Tech (8IADT) FIAP [(PDF)](https://github.com/marceloklotz/fiap-terceira-fase-ssp-df/blob/main/Desafio-8IADT-Fase3-TechChallenge-Secretaria.pdf).

## 👥 Integrantes do grupo
Os membros do grupo são compostos pelos seguintes servidores da Secretaria de Segurança Pública do Distrito Federal (SSP/DF):

- Alexandre Natã Vicente (**rm370024**) (ale.n.vicente@gmail.com)
- Antônio Cláudio Almeida (**rm370052**) (antonioalmeida@gmail.com)
- Cyd Ferreira Rodrigues (**rm370004**) (cydnelson@gmail.com)
- David Catherink (**rm369997**) (d.catherinck@gmail.com)
- Marcelo Macedo Klotz (**rm370010**) (marceloklotz@gmail.com)

## 🎲 Base de dados

Foi utilizado um dataset sintético (PubMedQA) servindo a dois propósitos complementares: (1) garantir cobertura de temas clinicamente críticos em português (o PubMedQA é majoritariamente em inglês); e (2) fornecer dados de treinamento baseados nas diretrizes brasileiras (FEBRASGO, INCA, Ministério da Saúde) que são as referências aplicáveis no contexto hospitalar nacional. Isso porque dados reais de pacientes são protegidos pela LGPD (Lei Geral de Proteção de Dados) e por normas do CFM (Conselho Federal de Medicina). Em um protótipo acadêmico é inviável usar prontuários reais. Dados sintéticos — gerados manualmente por especialistas ou com auxílio de IA, mas revisados — permitem desenvolver e testar pipelines sem expor informações sensíveis. Esta é prática padrão em pesquisa de IA em saúde.

O PubMedQA é um benchmark biomédico amplamente reconhecido na comunidade científica. Ele contém 1.000 perguntas clínicas extraídas de artigos publicados no PubMed (base de dados de literatura médica da Biblioteca Nacional de Medicina dos EUA).

O desafio exige que o fine-tuning seja realizado com 'dados específicos da área', e o PubMedQA fornece literatura biomédica revisada por pares, com fonte citável (PMID) — atendendo ao critério de “explainability”. Aproximadamente 27% dos registros cobrem temas de saúde feminina diretamente relevantes (ginecologia, obstetrícia, contracepção, câncer de mama, violência, saúde mental materna). O download é feito diretamente do GitHub oficial do projeto, sem necessidade de Google Drive.

O relatório técnico detalha como o código seleciona os registros para aplicar filtros relevantes, resultando em um subconjunto de registros biomédicos com alta relevância para o domínio do trabalho, que foram então convertidos para o formato interno do projeto. Além disso, trata do mapeamento das categorias e dos registros criados manualmente em português, baseados em diretrizes brasileiras e internacionais.
  
## 📒 Relatório técnico

O Relatório Técnico detalha a fundamentação teórica e a implementação prática do assistente, descrevendo uma arquitetura modular em cinco etapas: pré-processamento com anonimização (LGPD), fine-tuning com LoRA, recuperação de informações (RAG/FAISS), orquestração com LangChain e a criação de quatro fluxos clínicos via LangGraph.

O documento aprofunda a estratégia de dados híbrida, combinando literatura biomédica do PubMedQA com diretrizes brasileiras (FEBRASGO, INCA, OMS) em dados sintéticos, além de apresentar uma avaliação quantitativa abrangente por meio de métricas ROUGE, cobertura de termos médicos e uma rigorosa análise de bias e equidade demográfica. Por fim, o relatório discute as considerações éticas, a interpretabilidade das respostas (explainability) e os limites de atuação do protótipo como ferramenta de apoio à decisão.

O download do relatório pode ser feito diretamente pelo seguinte link: 
https://github.com/marceloklotz/fiap-terceira-fase-ssp-df

## 📽️ Vídeo explicativo

O vídeo explicativo sobre a metologia, resultados e notebook em execução foi disponbilizado a partir do seguinte link:


<p align="center">
  <img src="https://i.ytimg.com/vi/F-G5JFNiwdE/hqdefault.jpg" alt="FIAP - TECH CHALENGE (TERCEIRA FASE)">
</p>
<p align="center"> https://youtu.be/F-G5JFNiwdE </p>
