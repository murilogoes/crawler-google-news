
# Coletor de Notícias do Google News com Análise de Sentimento

Este projeto é um **crawler em Python** que busca notícias recentes no **Google News (RSS)** com base em um termo de busca, analisa o sentimento dos títulos utilizando um modelo de linguagem e salva os resultados em um arquivo de texto. 

O objetivo é facilitar o monitoramento e análise de temas de interesse na mídia, como instituições públicas, empresas ou acontecimentos recentes.

## Funcionalidades

> 💡 O projeto possui **duas abordagens para análise de sentimento**:
> - Uma com modelo local da Hugging Face (`nlptown/bert-base-multilingual-uncased-sentiment`)
> - Outra com **GPT-4 via API da OpenAI** para avaliação do sentimento institucional das manchetes


- Busca automatizada no Google News (últimas 24 horas)
- Conversão da data de publicação para o horário de Brasília
- Salvamento das notícias com título, mídia, data e link
- **Análise de sentimento** (positivo, neutro ou negativo) com o modelo `nlptown/bert-base-multilingual-uncased-sentiment`
- Geração de gráfico com a distribuição dos sentimentos

## Como funciona

Você pode escolher entre dois métodos para analisar o sentimento das manchetes:
- **Método 1**: Usar o modelo da Hugging Face localmente
- **Método 2 (alternativo)**: Enviar as manchetes para o GPT-4 via API da OpenAI, com um prompt que pergunta se a manchete representa positivamente, negativamente ou de forma neutra a instituição mencionada (ex: Polícia Militar)


O script realiza as seguintes etapas:

1. Monta a URL de busca no Google News com base no termo desejado
2. Faz uma requisição RSS e processa os dados XML
3. Extrai título, link, fonte e data de publicação
4. Converte o horário GMT para o fuso de Brasília
5. Salva tudo em um arquivo de texto (`noticias.txt`)
6. Lê esse arquivo, extrai os títulos e aplica análise de sentimento
7. Exibe os resultados em uma tabela e um gráfico

## Exemplo de saída

```
[12/05/2025 14:03:12] (G1) Polícia Militar realiza operação na zona norte de SP
https://g1.globo.com/noticia...
Sentimento: Positivo

[12/05/2025 12:45:02] (Estadão) Nova estratégia da PM em áreas de risco
https://estadao.com.br/noticia...
Sentimento: Neutro
```

## Pré-requisitos

- Python 3.7+
- Bibliotecas:
  - `requests`
  - `pytz`
  - `transformers`
  - `matplotlib`
  - `pandas`
  - `bs4` (se quiser expandir para scraping direto)

Instale os requisitos com:

```bash
pip install requests pytz transformers matplotlib pandas bs4
```

## Como usar

1. Clone este repositório
2. Execute o notebook no Jupyter ou Google Colab
3. Altere a variável `assunto` para o tema que deseja monitorar
4. Rode o código e o arquivo `noticias.txt` será criado
5. Em seguida, rode a célula de análise de sentimento para gerar a tabela e o gráfico

## Próximas etapas

- [ ] Enriquecer a análise com o conteúdo completo das notícias
- [ ] Geração de relatórios em PDF ou HTML
- [ ] Envio automático de alertas por Telegram ou e-mail

## Licença

Este projeto é de uso livre para fins acadêmicos e pessoais.

## Observação sobre a API da OpenAI

Para usar o GPT-4, você precisa:
1. Criar uma conta em [platform.openai.com](https://platform.openai.com)
2. Obter sua chave de API e inseri-la no código
3. Ter créditos ou um plano ativo na OpenAI

Este recurso é útil para avaliações institucionais mais precisas, considerando o contexto semântico de cada manchete.
