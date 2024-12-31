
# Tutorial para criação de projetos com Ruby on Rails (sem Ruby localmente)

Primeiramente, crie 'build' a seguinte Dockerfile com o comando:

Dockerfile:
```Dockerfile
# Use uma imagem oficial do Ruby
FROM ruby:3.2

# Instale dependências do sistema
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs yarn

# Defina o diretório de trabalho
WORKDIR /app

# Instale bundler e Rails
RUN gem install bundler rails

# Copie o Gemfile e Gemfile.lock (se existir)
COPY Gemfile Gemfile.lock /app/

# Instale as gems
RUN bundle install

# Copie o restante da aplicação para dentro do container
COPY . /app

```
Insira no seu terminal:
```bash 
$ docker build -t rails-crud 
```

Após isso, você já poderá criar seu projeto. Entre no diretório que deseja manter seu projeto, e insira no terminal:

```bash
$ docker run -it --rm -v $(pwd):/app -w /app rails-crud rails new nome-do-projeto
```
