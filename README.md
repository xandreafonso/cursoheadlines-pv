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

```shell
docker build -t cursoheadlines-pv .
```

## Rodar o container Docker

```shell
docker run -d --rm -p 80:80 --name cursoheadlines-pv cursoheadlines-pv
```

Acesse em http://localhost/curso-headlines


