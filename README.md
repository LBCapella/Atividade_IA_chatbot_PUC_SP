# Chatbot com Controle de Orçamento

Projeto 16 da disciplina de Inteligência Artificial, Ciência da Computação, PUC-SP.

Dupla: Luan Bonasorte Capella e Matheus Heimrath Barbosa

## Sobre

Chatbot feito em Python com o Ollama (modelo llama3.2:3b, grátis e rodando localmente), usando o SDK da OpenAI por meio da API compatível do Ollama. A cada mensagem ele mostra quantos tokens foram usados e quanto isso custaria em dólares, além do custo total da conversa. Como o Ollama é gratuito, o custo é simulado com os preços de referência do gpt-5-nano.

Como a API não guarda o histórico, a conversa inteira é reenviada a cada pergunta e o custo vai aumentando. Para controlar isso, quando o histórico passa de 1000 tokens, as mensagens antigas são resumidas pelo próprio modelo e só as mais recentes continuam inteiras.

## O que tem no notebook

- Classe `ChatOrcamento`, que guarda o histórico, calcula o custo e faz o resumo
- Conversa de teste com 12 perguntas
- Tabela com tokens e custo de cada chamada
- Gráficos de tokens por turno e custo acumulado
- Comparação entre a conversa com resumo e sem resumo
- Chat livre para testar

## Como rodar

### No Google Colab

1. Abrir o arquivo `Projeto16_Chatbot_Orcamento_Ollama.ipynb` no Google Colab
2. Em Ambiente de execução > Alterar tipo, escolher GPU T4 (funciona sem GPU, mas fica lento)
3. Rodar todas as células em ordem. A célula de instalação baixa o Ollama e o modelo, e leva alguns minutos a cada nova sessão

Não precisa de chave de API.

### Localmente

1. Instalar o Ollama e baixar o modelo: `ollama pull llama3.2:3b`
2. Criar o ambiente e instalar as dependências: `uv venv .venv && uv pip install -p .venv/bin/python -r requirements.txt`
3. Abrir com `jupyter lab` e rodar as células (a célula de instalação do Ollama só é necessária no Colab)

O arquivo `Projeto16_Chatbot_Orcamento.ipynb` é a versão original, que usa a API da OpenAI (gpt-5-nano) e a chave `OPENAI_API_KEY` nos Secrets do Colab.

## Configurações

No começo do notebook dá para mudar:

- `MODELO`: modelo usado (precisa estar baixado no Ollama)
- `PRECO_ENTRADA` e `PRECO_SAIDA`: preço de referência por 1 milhão de tokens, usado só para simular o custo
- `LIMITE_TOKENS`: limite que dispara o resumo
- `MANTER`: quantas mensagens recentes ficam sem resumir

## Tecnologias

Python, Ollama, OpenAI SDK, pandas e matplotlib.
