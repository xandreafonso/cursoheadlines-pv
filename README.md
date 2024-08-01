# Curso Avançado de Headlines

Essa é a página de vendas do meu curso para profissionais de marketing aprenderem sobre a criação de headlines persuasivas e criativas.

# Alterações

FAQ:
- Quanto tempo de acesso tem o curso?
- O Curso é sobre fórmulas de headlines?
- O que não é o curso?

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

Criar imagem usando o Caddy para integrar com Traefik:

```shell
docker build -f Dockerfile -t cursoheadlines-pv:v1.0 .
```

## Rodar o container Docker

```shell
docker run -d --rm -p 80:80 --name cursoheadlines-pv cursoheadlines-pv
```

Acesse em http://localhost/curso-headlines

# PUBLICAR COM PORTAINER + TRAEFIK

```shell
docker build -f Dockerfile -t cursoheadlines-pv:v1.1 .
docker tag cursoheadlines-pv:v1.1 xandreafonso/cursoheadlines-pv:v1.1
docker tag cursoheadlines-pv:v1.1 xandreafonso/cursoheadlines-pv:latest
docker login
docker push xandreafonso/cursoheadlines-pv:v1.1
docker push xandreafonso/cursoheadlines-pv:latest
```

Feito isso, preciso atualizar a Stack no Portainer.

# PUBLICAR SEM DOCKERHUB

```shell
docker save cursoheadlines-pv -o cursoheadlines-pv.tar
scp cursoheadlines-pv.tar root@5.161.117.216:/root/cursoheadlines-pv/
ssh root@5.161.117.216 "cd /root/cursoheadlines-pv/ && docker load -i cursoheadlines-pv.tar"
```

Feito isso, preciso atualizar a Stack no Portainer.

```shell
ssh root@5.161.117.216 "docker image prune -a -f"
```

# PUBLICAR SEM PORTAINER

```shell
docker save cursoheadlines-pv -o cursoheadlines-pv.tar
scp cursoheadlines-pv.tar root@5.161.117.216:/root/cursoheadlines-pv/
ssh root@5.161.117.216
cd /root/cursoheadlines-pv/
docker load -i cursoheadlines-pv.tar
docker stop cursoheadlines-pv
docker rm cursoheadlines-pv
docker run -d -p 80:80 -p 443:433 --name cursoheadlines-pv cursoheadlines-pv
docker image prune -a -f
```

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

# EXECUTAR A IMAGEM

```shell
docker run -d -p 80:80 -p 443:433 --name cursoheadlines-pv cursoheadlines-pv
```

# OUTROS

```shell
caddy file-server --browse --listen 9090
```

# ACESSAR PELA REDE LOCAL

## Roda o projeto na rede local

```shell
pnpm run dev --host
```

```shell
# Windows
netsh interface portproxy add v4tov4 listenport=5173 listenaddress=0.0.0.0 connectport=5173 connectaddress=IP_WSL

# Listar
netsh interface portproxy show all

# Deletar
netsh interface portproxy delete v4tov4 listenport=5173 listenaddress=0.0.0.0
```
