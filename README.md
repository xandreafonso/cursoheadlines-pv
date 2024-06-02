# Curso Avançado de Headlines

Essa é a página de vendas do meu curso para profissionais de marketing aprenderem sobre a criação de headlines persuasivas e criativas.

# EXECUTAR

## O path de acesso à página

Caso queira acessar a página pelo path "curso-headlines", crie o arquivo vite.config.js como abaixo:

```javascript
import { defineConfig } from 'vite';

export default defineConfig({
  base: '/curso-headlines',
  build: {
    outDir: 'dist/curso-headlines'
  }
});
```

Sem o arquivo acima, a página é acessada na raiz.

Nota: o path pode ser configurado pelo Traefik.

## Criar os arquivos de produção

```shell
pnpm run build
```

## Criar a imagem Docker

Criar imagem usando o Nginx:

```shell
docker build -f Dockerfile.nginx -t cursoheadlines-pv .
```

Criar imagem usando o Caddy:

```shell
docker build -f Dockerfile.caddy -t cursoheadlines-pv:v1.0 .
```

## Rodar o container Docker

```shell
docker run -d --rm -p 80:80 --name cursoheadlines-pv cursoheadlines-pv
```

Acesse em http://localhost/curso-headlines

## Enviar para o Docker Hub

```shell
docker tag cursoheadlines-pv:v1.0 xandreafonso/cursoheadlines-pv:v1.0
docker tag cursoheadlines-pv:v1.0 xandreafonso/cursoheadlines-pv:latest
```

Depois faz login no docker registry.

```shell
docker login
```

Depois envia as imagens.

```shell
docker push xandreafonso/cursoheadlines-pv:v1.0
docker push xandreafonso/cursoheadlines-pv:latest
```

# Executar a versão com Caddy

```shell
docker run -d -p 80:80 -p 443:433 --name cursoheadlines-pv xandreafonso/cursoheadlines-pv
```
