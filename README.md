# 🏫👨‍💻 Tech Challenge - Pós Tech (8IADT) FIAP - Fase 3: Assistente virtual de atendimento médico

Este repositório contém o notebook [FIAP_Fase_3.ipynb](https://github.com/marceloklotz/fiap-terceira-fase/blob/main/FIAP_Fase_3.ipynb) que apresenta o desenvolvimento de um protótipo de assistente virtual voltado para a saúde da mulher, com foco específico em triagem ginecológica e apoio à decisão clínica. O processo foi estruturado para aplicar os conceitos fundamentais da Fase 3 do curso, integrando ajuste fino de modelos, recuperação de informações e orquestração de fluxos complexos, conforme instruções contidas no [PDF](https://github.com/marceloklotz/fiap-terceira-fase/blob/main/8IADT-Fase3-TechChallenge-Secretaria.pdf).

O projeto seguiu uma metodologia dividida em etapas técnicas claras: 
- **Preparação do Ambiente:** Configuração do Google Colab com a instalação de bibliotecas essenciais como LangChain, LangGraph, Transformers e FAISS.
- **Criação de Dados Sintéticos:** Construção de um dataset especializado (health_qa.jsonl) contendo cerca de 100 exemplos de perguntas e respostas sobre temas como gestação, menopausa e violência doméstica para fundamentar o treinamento.
- **Ajuste Fino (Fine-tuning) com LoRA:** Utilização da técnica Low-Rank Adaptation (LoRA) para treinar o modelo base sshleifer/tiny-gpt2. Embora o modelo escolhido seja pequeno para permitir a execução em CPU, ele serviu como prova de conceito para o pipeline de treinamento.
- **Implementação de RAG (Retrieval-Augmented Generation):** Integração do modelo a uma base de conhecimento de protocolos clínicos usando a biblioteca FAISS para busca vetorial. Isso permite que o assistente recupere informações precisas de documentos antes de gerar uma resposta.
- **Orquestração com LangGraph:** Criação de um grafo de estados para gerenciar o fluxo de triagem. O sistema coleta sinais de alerta, avalia o nível de risco (Alto ou Baixo) e decide a conduta médica apropriada (encaminhamento urgente ou orientação de rotina).
- **Avaliação e Testes:** Execução de uma bateria de testes automatizados com cenários clínicos reais para validar a lógica de decisão e a acurácia da classificação de risco.

Link do notebook encontra-se disponível em:
https://github.com/marceloklotz/fiap-terceira-fase/blob/main/FIAP_Fase_3.ipynb

## 📝 Descrição do Desafio

A proposta do desafio foi desenvolver um assistente virtual médico personalizado, treinado com dados próprios da instituição, capaz de apoiar condutas clínicas, responder dúvidas de profissionais e sugerir procedimentos alinhados aos protocolos internos de atendimento feminino. O desafio também envolve a criação de fluxos automatizados, seguros e integrados, utilizando LangChain, para coordenar ações como verificação de exames ginecológicos pendentes, recomendação de tratamentos reprodutivos, emissão de alertas para possíveis casos de violência doméstica e articulação de atendimento multidisciplinar, considerando as particularidades e sensibilidades do cuidado à mulher.

Para tanto, utilizou-se o fine-tuning de LLMs com dados específicos da área e implementando fluxos automatizados de decisão clínica através do LangChain, sempre respeitando protocolos de segurança, privacidade e sensibilidade cultural específicos do atendimento feminino, conforme instruções da disciplina da Pós Tech (8IADT) FIAP [(PDF)](https://github.com/marceloklotz/fiap-terceira-fase/blob/main/8IADT-Fase3-TechChallenge-Secretaria.pdf).

## 👥 Integrantes do grupo
Os membros do grupo são compostos pelos seguintes servidores da Secretaria de Segurança Pública do Distrito Federal (SSP/DF):

- Alexandre Natã Vicente (**rm370024**) (ale.n.vicente@gmail.com)
- Antônio Cláudio Almeida (**rm370052**) (antonioalmeida@gmail.com)
- Cyd Ferreira Rodrigues (**rm370004**) (cydnelson@gmail.com)
- David Catherink (**rm369997**) (d.catherinck@gmail.com)
- Marcelo Macedo Klotz (**rm370010**) (marceloklotz@gmail.com)

## 🎲 Base de dados

O projeto fundamentou-se na criação de um conjunto de dados especializado chamado health_qa.jsonl, contendo aproximadamente 100 exemplos de perguntas e respostas estruturadas em formato de instrução. Os temas abrangem áreas críticas da saúde da mulher, como:
- Sinais de alerta na gestação e puerpério
- Protocolos de conduta em casos de violência doméstica
- Orientações sobre contracepção, menopausa e saúde mental materna
- Rastreamento preventivo de câncer de colo do útero e de mama

Utilizando a técnica LoRA (Low-Rank Adaptation) no modelo base sshleifer/tiny-gpt2, o processo de treinamento gerou os seguintes indicadores técnicos:

Parâmetros Treináveis: Apenas 64 parâmetros foram ajustados, representando cerca de 0,03% do total do modelo, o que permitiu a execução em ambiente de CPU.
Performance de Treinamento: Após duas épocas, a função de perda (loss) estabilizou em aproximadamente 10,74.
Nota Técnica: Embora o modelo gerado seja um protótipo de baixa fidelidade semântica devido ao seu tamanho reduzido, ele valida com sucesso o pipeline técnico de especialização para o domínio da saúde.

Foi gerada uma base de conhecimento baseada em protocolos clínicos simplificados, indexada para o sistema de Geração Aumentada por Recuperação (RAG).
- **Vetorização:** Os documentos foram transformados em vetores numéricos usando o modelo de embedding all-MiniLM-L6-v2.
- **Indexação:** Utilizou-se a biblioteca FAISS para permitir buscas semânticas ultrarrápidas, recuperando trechos dos protocolos em milissegundos para embasar as respostas da IA.

O sistema de triagem, orquestrado pelo LangGraph, foi submetido a uma bateria de testes com cinco cenários clínicos reais (como suspeita de pré-eclâmpsia e rastreamento atrasado). Os dados de saída revelaram:

- Acurácia na Classificação de Risco: 100% de precisão na distinção entre risco "ALTO" e "BAIXO".
- Acurácia na Escolha de Conduta: 100% de sucesso na seleção entre encaminhamento urgente ou orientação de rotina.
- Segurança e Anonimização: O pipeline aplicou com sucesso a detecção e remoção de dados sensíveis (CPFs, e-mails, telefones) via expressões regulares antes do processamento.

Os dados gerados reforçam um modelo de governança clínica onde:
- Casos de alto risco acionam regras determinísticas e não dependem da geração criativa da LLM, garantindo encaminhamento imediato.
- Regras de segurança estão codificadas diretamente no prompt para impedir diagnósticos definitivos ou prescrições medicamentosas pelo assistente.
  
## 📒 Relatório técnico

O relatório técnico descreve o desafio proposto e a forma de exploração de dados adotada pelos membros do grupo, explicando as estratégias de pré-processamento e limpeza dos dados, os modelos avaliados e utilizados, os resultados obtidos, a interpretação do dados, além da aplicabilidade prática e as lições aprendidas durante o desenvolvimento da atividade acadêmica.

O download do relatório pode ser feito diretamente pelo seguinte link: 
https://github.com/marceloklotz/fiap-terceira-fase/blob/main/Relatorio-Tecnico-Terceira-Fase.pdf

## 📽️ Vídeo explicativo

O vídeo explicativo sobre a metologia, resultados e notebook em execução foi disponbilizado a partir do seguinte link:

![FIAP - TECH CHALLENGE (TERCEIRA FASE)](https://i.ytimg.com/vi/4wX8KIxYdJ4/maxresdefault.jpg)

<p align="center"> https://youtu.be/4wX8KIxYdJ4 </p>
