# web-camadas-adone

## Banco de dados local

No meu projeto final utilizei o MySQL rodando localmente na minha máquina junto com o Prisma ORM. Durante o desenvolvimento utilizei o Prisma Studio para visualizar e gerenciar os dados do banco.

A conexão com o banco local era feita através da variável `DATABASE_URL` no arquivo `.env`, apontando para o localhost da máquina.

O Prisma era responsável por criar e gerenciar as tabelas automaticamente com base no arquivo `schema.prisma` do projeto.

Abaixo estão alguns prints do banco local, do schema do Prisma e das tabelas criadas.

### Print do arquivo .env

<img width="1788" height="1005" alt="print  env" src="https://github.com/user-attachments/assets/f20afa64-174e-4223-91c0-72442044f50b" />


### Print do schema.prisma

<img width="1475" height="906" alt="print schemaprisma" src="https://github.com/user-attachments/assets/6cf8f0f7-1ace-4487-9354-29fcae9cd0e9" />


### Print do banco local funcionando

<img width="1884" height="937" alt="print banco local" src="https://github.com/user-attachments/assets/4085fc97-403d-4705-97ee-c657c6ef9492" />


## Opções de hospedagem pesquisadas

### Railway

O Railway oferece hospedagem gratuita de banco MySQL com integração simples e rápida. A plataforma gera automaticamente a connection string necessária para conexão remota e possui compatibilidade com Prisma.

Escolhi utilizar o Railway no projeto pois apresentou configuração mais simples e conexão estável no ambiente utilizado.

---

### Supabase

O Supabase oferece banco PostgreSQL gratuito com limite de armazenamento e conexões no plano free. Também possui compatibilidade com Prisma.

Apesar de ser uma plataforma muito utilizada, optei por não utilizar porque meu projeto já estava estruturado utilizando MySQL.

---

### Aiven

O Aiven oferece serviços de banco de dados como MySQL e PostgreSQL em nuvem. A plataforma possui recursos mais próximos de um ambiente profissional e permite configuração de SSL e acesso remoto.

Inicialmente considerei utilizar o Aiven porque já tinha tido contato com a plataforma anteriormente em outro projeto. Porém, durante os testes encontrei dificuldades relacionadas à conexão remota e SSL no ambiente utilizado.

## Hospedagem do banco de dados

Para hospedar o banco de dados do meu projeto utilizei o Railway.

Primeiramente criei uma conta na plataforma e em seguida criei um serviço MySQL dentro do projeto.

### Print do banco criado no Railway

<img width="1918" height="930" alt="raiway banco 2" src="https://github.com/user-attachments/assets/64e92b9e-d102-4fe6-8bb4-e286c24ec97f" />



Após a criação do banco, o Railway disponibilizou automaticamente as informações de conexão, como host, porta, usuário, senha e nome do banco de dados.

### Print da connection string do Railway

<img width="1911" height="991" alt="railway banco" src="https://github.com/user-attachments/assets/17ad943f-dd17-4699-b6a4-572ff63e86fc" />


Com esses dados, atualizei a variável `DATABASE_URL` no arquivo `.env` para apontar para o banco remoto hospedado na nuvem.

Depois disso executei o comando:

```bash
npx prisma db push
```

Esse comando criou automaticamente todas as tabelas do projeto no banco remoto com base no schema do Prisma.

### Print do comando prisma db push funcionando

<img width="706" height="262" alt="print cmd" src="https://github.com/user-attachments/assets/6e32b2b7-0a11-485a-88b7-0c899c8f638a" />


Após a sincronização do banco, utilizei o Prisma Studio e também realizei testes nas rotas da API para confirmar que as requisições estavam funcionando corretamente utilizando o banco remoto.

### Print do banco remoto funcionando

<img width="1894" height="873" alt="api funcionando banco" src="https://github.com/user-attachments/assets/15b3c83e-0d54-4cfe-8aa0-a7eb1dce07cb" />

### Print da API funcionando

<img width="1836" height="1001" alt="api funcionando" src="https://github.com/user-attachments/assets/689cc00f-1d7a-4f24-a3b3-a22e16208eb6" />


### Print dos dados aparecendo no banco remoto

<img width="1892" height="950" alt="image" src="https://github.com/user-attachments/assets/5f37f980-cf73-4b44-94cc-8663fbb01753" />

## Diferenças entre banco local e remoto

### Connection string

A connection string é uma URL utilizada pela aplicação para realizar a conexão com o banco de dados.

Nela ficam informações importantes como:

* tipo do banco
* usuário
* senha
* host
* porta
* nome do banco

No ambiente local a conexão apontava para o localhost da minha máquina. Já no ambiente remoto a conexão passou a utilizar o endereço fornecido pelo Railway.

---

### Uso do arquivo .env

O arquivo `.env` é utilizado para armazenar informações sensíveis da aplicação, principalmente a connection string do banco de dados.

Esse arquivo não deve ser enviado para o GitHub porque contém dados privados como usuário e senha do banco.

Por esse motivo, cada ambiente pode possuir uma configuração diferente de banco sem precisar alterar diretamente o código da aplicação.

---

### Dados do banco

Os dados existentes no banco local não foram enviados automaticamente para o banco remoto.

Isso acontece porque os dois bancos funcionam em ambientes separados.

Para transferir os dados seria necessário realizar exportação e importação manual ou utilizar ferramentas de migração de dados.

---

### Problemas encontrados

Durante o processo tentei inicialmente utilizar o Aiven para hospedar o banco de dados remoto.

Porém encontrei dificuldades de conexão com o Prisma. O erro apresentado era o `P1001`, indicando que a aplicação não conseguia acessar o servidor remoto do banco de dados.

Foram realizados testes de conexão via terminal e verificações relacionadas à porta e SSL da conexão remota.

### Print do erro P1001

<img width="840" height="205" alt="print erro aiven" src="https://github.com/user-attachments/assets/ac6f90da-1b6b-488d-b7ca-3cca90bbe830" />


Após os testes, optei por utilizar o Railway como alternativa, pois apresentou integração mais simples com o Prisma e conexão funcionando corretamente no ambiente utilizado.

Com a atualização da `DATABASE_URL` utilizando os dados fornecidos pelo Railway, consegui executar o comando `npx prisma db push` sem problemas e criar as tabelas remotamente.
