## Instalação e Configuração
Pré-Requisitos:
* [Python 2](https://www.python.org/downloads/)
* [virtualenv](https://virtualenv.pypa.io/en/stable/)
* [MySQL Server](https://dev.mysql.com/downloads/mysql/)
* Não se esqueça de adiciona-los ao PATH do sistema.

Clone o repositório do GitHub:
```
git clone https://github.com/samuel-messias1999/projeto-transportadora
```

Apague as pastas ".idea" e "venv". Após isso, crie um ambiente virtual para o projeto e o ative:
```
virtualenv projeto-transportadora
source projeto-transportadora/bin/activate
```

Instale os pacotes necessários:
```
pip install -r requirements.txt
```

## Configuração do Banco de Dados
Você vai precisar criar um usuário MySQL pelo terminal, bem como um banco de dados MySQL. Feito isso, conceda todos os privilégios do banco de dados criado a seu usuario, dessa forma:

```
$ mysql -u root

mysql> CREATE USER 'dt_admin'@'localhost' IDENTIFIED BY 'dt2016';

mysql> CREATE DATABASE dreamteam_db;

mysql> GRANT ALL PRIVILEGES ON dreamteam_db . * TO 'dt_admin'@'localhost';
```

Após isso, execulte as seguintes migrações:

* `flask db migrate`
* `flask db upgrade`

Caso ocorra problemas, defina as variáveis da etapa "Execultando o Programa" logo abaixo primeiro, e tente execultar as migrações novamente.

## Instância/Arquivo config.py
Crie um diretório, `instance`, e nele crie o arquivo `config.py`. Esse arquivo deve conter configurações das variáveis que não devem ser compartilhadas publicamente, como senhas e chaves secretas. Essa aplicação requer que você tenha as seguintes configurações de variáveis:
* `SECRET_KEY = 'p9Bv<3Eid9%$i01'` ou outra chave secreta.
* `SQLALCHEMY_DATABASE_URI ('mysql://dt_admin:dt2016@localhost/dreamteam_db')` se usando Linux.
* `SQLALCHEMY_DATABASE_URI ('mysql://dt_admin:dt2016@127.0.0.1/dreamteam_db')` se usando Windows.

## Execultando o Programa
Defina as variáveis FLASK_APP e FLASK_CONFIG como a seguir:

Se usando Linux:
* `export FLASK_APP=run.py`
* `export FLASK_CONFIG=development`

Se usando Windows:
* `set FLASK_APP=run.py`
* `set FLASK_CONFIG=development`

Você pode agora execultar a aplicação usando o seguinte comando: `flask run`

## Testando
Primeiro, crie um banco de dados para testes e conceda todos os privilégios do banco a seu usuário, como a seguir:

```
$ mysql -u root

mysql> CREATE DATABASE dreamteam_test;

mysql> GRANT ALL PRIVILEGES ON dreamteam_test . * TO 'dt_admin'@'localhost';
```

Para testar, execulte o seguinte comando: `python tests.py`

## Feito Com...
* [Flask](http://flask.pocoo.org/)
