# conceitos-docker

# Aula de Docker: Conceitos Básicos e Exemplo Prático

## 1. O que é Docker?

Docker é uma plataforma de software que permite desenvolver, empacotar e executar aplicativos de forma isolada, em containers. Esses containers são ambientes leves e portáveis que garantem que o aplicativo funcione de maneira consistente em qualquer lugar, desde o ambiente de desenvolvimento até a produção.

### Principais Conceitos do Docker:

- **Imagem (Image)**: Uma imagem é um pacote imutável contendo tudo o que é necessário para rodar um aplicativo (código, bibliotecas, dependências, etc.). As imagens são usadas para criar containers.

- **Container**: Um container é uma instância executável de uma imagem. Ele é um ambiente isolado onde o aplicativo roda de maneira consistente, independentemente do sistema operacional ou ambiente.

- **Dockerfile**: É um arquivo de texto que contém instruções para construir uma imagem Docker. Ele define o ambiente de execução do aplicativo, incluindo quais dependências instalar, como configurar e como iniciar o aplicativo.

- **Docker Hub**: Um repositório online de imagens Docker, onde você pode encontrar imagens oficiais de várias ferramentas e aplicativos ou subir as suas próprias imagens.

- **Volume**: Um volume é um diretório persistente usado por containers para armazenar dados. Diferente dos containers, os volumes não são destruídos quando o container é removido.

---

## 2. Instalando o Docker

Para começar a usar o Docker, você deve instalá-lo em seu sistema. O processo de instalação pode variar dependendo do seu sistema operacional. Confira os links oficiais para os tutoriais de instalação:

- [Docker para Linux](https://docs.docker.com/engine/install/)
- [Docker para Windows](https://docs.docker.com/desktop/install/windows-install/)
- [Docker para Mac](https://docs.docker.com/desktop/install/mac-install/)

---

## 3. Comandos Básicos do Docker

Aqui estão alguns comandos essenciais do Docker:

- **`docker --version`**: Verifica a versão do Docker instalada.
- **`docker pull <nome-da-imagem>`**: Baixa uma imagem do Docker Hub para o seu sistema local.
- **`docker build -t <nome-da-imagem> .`**: Cria uma imagem a partir de um Dockerfile presente no diretório atual.
- **`docker run <nome-da-imagem>`**: Cria e executa um container a partir de uma imagem.
- **`docker ps`**: Lista os containers em execução.
- **`docker stop <id-do-container>`**: Para a execução de um container.
- **`docker rm <id-do-container>`**: Remove um container parado.
- **`docker rmi <nome-da-imagem>`**: Remove uma imagem do sistema.

---

## 4. Exemplo Prático: Criando um Aplicativo Simples com Docker

Vamos criar um exemplo prático de como usar o Docker para rodar uma aplicação simples.

### 4.1. Criando o Dockerfile

Crie um diretório para o seu projeto e dentro dele, crie um arquivo chamado `Dockerfile`. O conteúdo desse arquivo será o seguinte:

```Dockerfile
# Usando uma imagem base do Python
FROM python:3.9-slim

# Definindo o diretório de trabalho dentro do container
WORKDIR /app

# Copiando o arquivo de requisitos para o container
COPY requirements.txt .

# Instalando as dependências
RUN pip install -r requirements.txt

# Copiando o código da aplicação para o container
COPY . .

# Expondo a porta 5000
EXPOSE 5000

# Comando para rodar a aplicação
CMD ["python", "app.py"]
