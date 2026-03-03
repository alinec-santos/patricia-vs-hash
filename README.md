# Patricia vs Hash - Indice Invertido para Busca Textual

Este projeto foi desenvolvido como Trabalho Pratico 1 da disciplina de Algoritmos e Estruturas de Dados 2 (AEDS 2) na Universidade Federal de Vicosa (UFV) - Campus Florestal. O objetivo principal foi implementar e comparar duas tecnicas de indexacao e busca em grandes conjuntos de dados textuais: a arvore Patricia e a tabela hash, aplicadas a construcao de um indice invertido.

## 1. Descricao do Projeto

O sistema implementa um indice invertido, estrutura fundamental em sistemas de recuperacao de informacao, que mapeia cada palavra unica para a lista de documentos (e posicoes) onde ela ocorre. Foram implementadas duas abordagens concorrentes:

- Arvore PATRICIA (Practical Algorithm to Retrieve Information Coded in Alphanumeric): Estrutura compacta baseada em arvore binaria que armazena strings de forma eficiente, compartilhando prefixos comuns.
- Tabela HASH: Estrutura que utiliza uma funcao de dispersao para distribuir as palavras em buckets, com tratamento de colisoes por listas encadeadas.

O programa permite inserir documentos textuais, construir os indices invertidos em ambas as estruturas e realizar consultas, medindo e comparando o desempenho em termos de numero de comparacoes durante insercoes e buscas.

## 2. Objetivos

- Implementar uma arvore PATRICIA do zero para armazenamento de strings e listas de ocorrencias
- Implementar uma tabela HASH com funcao de dispersao e tratamento de colisoes
- Construir indices invertidos completos a partir de documentos de texto
- Medir e comparar o numero de comparacoes realizadas em operacoes de insercao e busca em ambas as estruturas
- Analisar as vantagens e desvantagens de cada abordagem para diferentes cenarios


## 3. Detalhes Tecnicos de Implementacao

### 3.1 Arvore PATRICIA

A implementacao da arvore Patricia segue o conceito de busca por comparacao de caracteres em posicoes especificas:

**Estrutura dos nos:**
- No Interno: Contem um caractere de decisao e ponteiros para filhos (esquerda/direita)
- No Folha (Externo): Armazena a palavra completa e sua lista de ocorrencias

**Funcionamento da Busca:**
1. Inicia na raiz da arvore
2. Se for no externo: compara a palavra buscada com a armazenada
3. Se for no interno: compara o caractere na posicao indicada
4. Decide se vai para o filho esquerdo ou direito
5. Repete ate encontrar um no externo ou constatar ausencia

**Insercao:** Novos termos sao inseridos comparando-se os caracteres e criando novos nos internos e folhas conforme necessario para representar prefixos compartilhados.

### 3.2 Tabela HASH

A tabela hash utiliza um vetor de listas encadeadas (buckets) para armazenar as entradas:

**Estrutura:**
- Vetor de tamanho fixo (ex: 10007 posicoes)
- Cada posicao contem uma lista encadeada de entradas
- Cada entrada: { palavra, lista de ocorrencias }

**Funcao Hash:** Transforma a palavra (string) em um indice inteiro dentro do intervalo da tabela.

**Tratamento de Colisoes:** Por listas encadeadas (encadeamento separado). Quando duas palavras diferentes resultam no mesmo indice, sao armazenadas na mesma posicao, em sequencia.

### 3.3 Contadores de Desempenho

Foram implementados contadores especificos para medir:

| Operacao | Patricia | Hash |
|----------|----------|------|
| Insercao | Numero de comparacoes de caracteres ate encontrar posicao | Numero de comparacoes de strings na lista do bucket |
| Busca | Numero de comparacoes de caracteres no percurso | Numero de comparacoes de strings na lista do bucket |

## 4. Compilacao e Execucao

O projeto utiliza um Makefile para facilitar a compilacao:

```bash
# Compilar o projeto
make all

# Executar o programa
./programa

# Limpar arquivos compilados
make clean
