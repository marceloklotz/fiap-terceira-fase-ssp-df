# 🏫👨‍💻 Tech Challenge - Pós Tech (8IADT) FIAP - Fase 3: Assistente virtual de atendimento médico

Este repositório contém o notebook [FIAP_Fase_3.ipynb](https://github.com/marceloklotz/fiap-terceira-fase-ssp-df) que apresenta o desenvolvimento de um protótipo de assistente virtual voltado para a saúde da mulher, com foco específico em triagem ginecológica e apoio à decisão clínica. O processo foi estruturado para aplicar os conceitos fundamentais da Fase 3 do curso, integrando ajuste fino de modelos, recuperação de informações e orquestração de fluxos complexos, conforme instruções contidas no [PDF](https://github.com/marceloklotz/fiap-terceira-fase-ssp-df/blob/main/Desafio-8IADT-Fase3-TechChallenge-Secretaria.pdf).

O projeto seguiu uma metodologia dividida em etapas técnicas claras: 
- **Preparação do Ambiente:** Configuração do Google Colab com a instalação de bibliotecas essenciais como LangChain, LangGraph, Transformers e FAISS.
- **Criação de Dados Sintéticos:** Construção de um dataset especializado (health_qa.jsonl) contendo cerca de 100 exemplos de perguntas e respostas sobre temas como gestação, menopausa e violência doméstica para fundamentar o treinamento.
- **Ajuste Fino (Fine-tuning) com LoRA:** Utilização da técnica Low-Rank Adaptation (LoRA) para treinar o modelo base sshleifer/tiny-gpt2. Embora o modelo escolhido seja pequeno para permitir a execução em CPU, ele serviu como prova de conceito para o pipeline de treinamento.
- **Implementação de RAG (Retrieval-Augmented Generation):** Integração do modelo a uma base de conhecimento de protocolos clínicos usando a biblioteca FAISS para busca vetorial. Isso permite que o assistente recupere informações precisas de documentos antes de gerar uma resposta.
- **Orquestração com LangGraph:** Criação de um grafo de estados para gerenciar o fluxo de triagem. O sistema coleta sinais de alerta, avalia o nível de risco (Alto ou Baixo) e decide a conduta médica apropriada (encaminhamento urgente ou orientação de rotina).
- **Avaliação e Testes:** Execução de uma bateria de testes automatizados com cenários clínicos reais para validar a lógica de decisão e a acurácia da classificação de risco.

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

O relatório técnico detalha como o código seleciona os registros para aplicar filtros relevantes, resultando em um subconjunto de registros biomédicos com alta relevância para o domínio do trabalho, que foram então convertidos para o formato interno do projeto.
  
## 📒 Relatório técnico

O relatório técnico descreve o desafio proposto e a forma de exploração de dados adotada pelos membros do grupo, explicando as estratégias de pré-processamento e limpeza dos dados, os modelos avaliados e utilizados, os resultados obtidos, a interpretação do dados, além da aplicabilidade prática e as lições aprendidas durante o desenvolvimento da atividade acadêmica.

O download do relatório pode ser feito diretamente pelo seguinte link: 
https://github.com/marceloklotz/fiap-terceira-fase/blob/main/Relatorio-Tecnico-Terceira-Fase.pdf

## 📽️ Vídeo explicativo

O vídeo explicativo sobre a metologia, resultados e notebook em execução foi disponbilizado a partir do seguinte link:

![FIAP - TECH CHALLENGE (TERCEIRA FASE)](https://i.ytimg.com/vi/4wX8KIxYdJ4/maxresdefault.jpg)

<p align="center"> https://youtu.be/4wX8KIxYdJ4 </p>
