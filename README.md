# web-camadas-adone

## Banco de dados local

No meu projeto final eu utilizei o MySQL rodando localmente na minha máquina usando o Prisma e a 
interface dele o Prisma Studio.

A conexão com o banco era feita através da variável DATABASE_URL no arquivo .env, apontando para o localhost.

O Prisma era responsável por gerenciar as tabelas com base no schema.prisma.

Abaixo estão alguns prints do banco local e das tabelas criadas.


- PRINTS AQ



## Opções de hospedagem

### Railway
O Railway oferece banco MySQL gratuito com algumas limitações de uso. É compatível com Prisma e possui integração simples.

Considerei utilizar essa opção pela facilidade, porém optei por outra plataforma para testar uma configuração diferente.

---

### Supabase
O Supabase oferece banco PostgreSQL gratuito, com limite de armazenamento e conexões. Funciona com Prisma, porém utiliza PostgreSQL ao invés de MySQL.

Não utilizei pois meu projeto já estava estruturado com MySQL.

---

### Aiven
O Aiven oferece serviços de banco como MySQL e PostgreSQL, com plano gratuito por tempo limitado.

Escolhi utilizar o Aiven para testar a conexão com um banco remoto mais próximo de um ambiente real, mesmo sendo um pouco mais complexo de configurar.
E também foi o que o professor me auxiliou a configurar em um outro projeto meu, então tenho mais familiaridade.



## Hospedagem do banco de dados

Para hospedar o banco de dados do meu projeto, utilizei o Aiven.

Primeiramente, criei uma conta na plataforma e em seguida criei um serviço de banco MySQL.

Após a criação, o Aiven disponibilizou as informações de conexão, como host, porta, usuário, senha e nome do banco.

Com esses dados, montei a connection string e atualizei a variável DATABASE_URL no arquivo .env do meu projeto para apontar para o banco remoto.

Depois disso, executei o comando do Prisma para criar as tabelas no banco remoto.

Após a criação das tabelas, testei a API e as requisições funcionaram normalmente utilizando o banco hospedado na nuvem.


- PRINTS AQ


## Diferenças entre banco local e remoto

### Connection string

A connection string é basicamente uma URL que a aplicação usa para se conectar ao banco de dados.

Nela ficam informações importantes como o tipo do banco (no meu caso MySQL), o usuário, a senha, o host (endereço do servidor), a porta e o nome do banco.

No ambiente local, essa conexão apontava para o localhost, já no banco remoto passou a apontar para o servidor do Aiven.

---

### Uso do .env

O arquivo .env é utilizado para guardar dados sensíveis da aplicação, como a connection string do banco.

Ele não é enviado para o GitHub porque contém informações como usuário e senha do banco, o que poderia comprometer a segurança do sistema.

Por isso, cada ambiente (local ou remoto) pode ter um .env diferente sem precisar alterar o código.

---

### Dados do banco

Os dados que estavam no banco local não foram automaticamente para o banco remoto.

Isso acontece porque são dois bancos diferentes, em ambientes separados.

Para transferir os dados seria necessário fazer exportação e importação manual, o que não foi feito nesse caso.

---

### Problemas encontrados

Durante o processo tive dificuldade para conectar ao banco remoto do Aiven.

Inicialmente a conexão não funcionava corretamente por conta da configuração de segurança (SSL).

Após ajustar a connection string com os parâmetros corretos, consegui conectar normalmente e executar as migrations do Prisma no banco remoto.

