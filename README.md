# NestJS - Swagger - Documentação de Endpoint

O Swagger (*aka* OpenApi) é uma biblioteca muito conhecida no universo backend, estando disponível para diversas linguagens e frameworks. Ela gera um site interno no seu backend que descreve, com muitos detalhes, cada endpoint e estrutura de entidades presentes na sua aplicação.

Além disso, também oferece uma interface para que a API seja testada, sem precisar de um cliente HTTP externo (*aka* Postman, Insomnia, Thunder Client, etc) e, principalmente, com configuração ZERO!

Como de costume, o Nest resolve toda a parte chata da configuração e a gente só precisa declarar algumas linhas de código para integrar essa poderosa API.

## Instalação

- `@nestjs/swagger`
- `swagger-ui-express`

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

> Também é possível usar o Swagger no Nest com o Fastify, basta usar a lib do swagger `fastify-swagger`

## Configuração

Abra o arquivo `main.ts` e adicione o seguinte conteúdo:

```typescript
import { NestFactory } from '@nestjs/core';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Documentação com Swagger - Fábrica de Sinapse')
    .setDescription(
      'O Swagger (aka OpenApi) é uma biblioteca muito conhecida no universo backend, estando disponível para diversas linguagens e frameworks. Ela gera um site interno no seu backend que descreve, com muitos detalhes, cada endpoint e estrutura de entidades presentes na sua aplicação.',
    )
    .setVersion('1.0')
    .addTag('users')
    .addTag('pokemons')
    .addTag('types')
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, document);

  await app.listen(3000);
}

bootstrap();
```

## Acessando

Execute a aplicação

```bash
npm run start:dev
```

Abra a URL no seu navegador

http://localhost:3000/api/

Pronto!

![image-20211023123352769](C:\GitHub\FabricaDeSinapse_Videos\nestjs-documentacao-swagger\images\image-20211023123352769.png)

## Tags

As tags servem para organizar endpoints.

Elas são declaradas no `main.ts` e utilizadas nos `controllers`.

### Vamos gerar um recurso

- `users`

```bash
nest g resource users
```

