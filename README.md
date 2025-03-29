# conceitos-docker

# Conceitos Básicos e Exemplo Prático

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

Exemplos de docker pull [docker pull] (https://github.com/Macelot/manual-docker)

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
```

-------

## Componentes Essenciais do Docker

### Imagens Docker

São modelos prontos para criar containers. Pense nelas como "fotografias" do ambiente necessário para rodar um software.

### Containers Docker

São instâncias de imagens que executam um aplicativo isoladamente.

### Dockerfile

Um arquivo que define como a imagem Docker será construída.

### Docker Compose

Permite orquestrar múltiplos containers, útil para aplicações que precisam de vários serviços (exemplo: um app web, um banco de dados e um serviço de cache).


## Exemplo Prático: Criando um Site com Flask e Docker

Agora, vamos surpreender seus alunos mostrando como criar uma aplicação web em Flask e rodá-la dentro de um container Docker.

** 1. Criando o Projeto

Crie uma pasta chamada meu_projeto_docker e dentro dela, crie os seguintes arquivos:

Dockerfile

app.py

requirements.txt

docker-compose.yml


** 2. Criando o Arquivo de Dependências

O arquivo requirements.txt deve conter:

flask

Isso indica que precisamos instalar o Flask dentro do nosso container.

** 3. Criando a Aplicação Flask

O arquivo app.py conterá um pequeno servidor web:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "🚀 Olá, mundo! Seu site Flask está rodando no Docker! 🔥"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

Essa aplicação Flask cria uma página simples que exibe uma mensagem.

** 4. Criando o Dockerfile

O Dockerfile define como nosso ambiente será configurado:

# Usando uma imagem base do Python
```python
FROM python:3.9-slim
```

# Definindo o diretório de trabalho dentro do container
```python
WORKDIR /app
```
# Copiando os arquivos do projeto
```python
COPY requirements.txt .
```
# Instalando as dependências
```python
RUN pip install -r requirements.txt
```
# Copiando o código da aplicação
```python
COPY . .
```
# Expondo a porta 5000
```python
EXPOSE 5000
```
# Comando para iniciar a aplicação
```
CMD ["python", "app.py"]
```

** 5. Criando o Docker Compose (Opcional, mas útil!)

O docker-compose.yml permite rodar nosso app de maneira ainda mais fácil:
```python
version: '3.8'

services:
  app:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    environment:
      - FLASK_ENV=development
```

** 6. Executando o Projeto

Agora, com tudo pronto, abra o terminal e execute os seguintes comandos:

Criar a imagem Docker (este texto meu-flask-app é apenas para exibição no Docker Desktop e posteriormente ser chamado pelo comando seguinte)
```python
docker build -t meu-flask-app .
```

Rodar o container
```python
docker run -p 5000:5000 meu-flask-app
```

Agora, abra o navegador e acesse:
🌍 http://localhost:5000

Você verá a mensagem:
🚀 "Olá, mundo! Seu site Flask está rodando no Docker!" 🔥

Conclusão

Esse exemplo mostra como podemos empacotar um site Flask dentro de um container e executá-lo de forma portável e escalável. Agora imagine... Se fosse uma API, um banco de dados, ou até mesmo um ambiente de produção completo? O Docker torna tudo isso simples e poderoso!


Próximos passos: [docker pull] (https://github.com/Macelot/manual-docker)
