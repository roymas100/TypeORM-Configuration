# TypeORM-Configuration

# Tabela de conteúdos
  * [Configurando TypeORM](#ancora1)
  * [Exemplo de migration de criação](#ancora2)
  * [Commandos de typeorm para migrations](#ancora3)
  * [Configurando Models](#ancora4)
  
<a id="ancora1"></a>
# Configurando TypeORM

#### Instale as dependencias

```
yarn add typeorm pg reflect-metadata
```

#### Configuração do ```ormconfig.json``` para postgress

```
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "docker",
  "database": "gostack_gobarber",
  "entities": [
    "./src/models/*.ts"
  ],
  "migrations": [
    "./src/database/migrations/*.ts"
  ],
  "cli": {
    "migrationsDir": "./src/database/migrations"
  }
}
```

#### Crie uma pasta ```./src/database```, e no seu index coloque o codigo abaixo:

```
import { createConnection } from 'typeorm'

createConnection();
```

#### Crie uma pasta ```./src/databe/migrations```

#### No ```package.json```, crie um script

```
...
"scripts" : {
  ...
  "typeorm": "ts-node-dev ./node_modules/typeorm/cli.js",
  ...
}
...
```

#### Criando migrations após configuração

```
yarn typeorm migration:create -n CreateAppointments
```

<a id="ancora2"></a>
# Example de migration: 

```
import { MigrationInterface, QueryRunner, Table } from "typeorm";

export class CreateAppointments1608663619421 implements MigrationInterface {

    public async up(queryRunner: QueryRunner): Promise<void> {
      await queryRunner.createTable(
        new Table({
          name: 'appointments',
          columns: [
            {
              name: 'id',
              type: 'varchar',
              isPrimary: true,
              generationStrategy: 'uuid',
            },
            {
              name: 'provider',
              type: 'varchar',
              isNullable: false,
            },
            {
              name: 'date',
              type: 'timestamp with time zone',
              isNullable: false,
            }
          ]
        })
      );
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
      await queryRunner.dropTable('appointments');
    }
}
```

<a id="ancora3"></a>
# Commandos de typeorm para migrations:

<b>1. Executar migrations: </b>

```
yarn typeorm migration:run
```

<b>2. Reverter ultima migrations: </b>

```
yarn typeorm migration:revert
```

<b>3. Mostrar log de migrations: </b>

```
yarn typeorm migration:show
```

<a id="ancora4"></a>
# Configurando Models

#### Em ```tsconfig.json```, habilite as configs descritas abaixo:

```
{
  ...
  "strictPropertyInitialization": false,  /* Enable strict checking of property initialization in classes. */
  ...
  "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
  "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */
  ...
}
```
