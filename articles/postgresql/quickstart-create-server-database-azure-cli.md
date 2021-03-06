---
title: 'Início Rápido: criar um Banco de Dados do Azure para PostgreSQL usando a CLI do Azure'
description: Guia de início rápido para criar e gerenciar o servidor do Banco de Dados do Azure para PostgreSQL usando a CLI (interface de linha de comando) do Azure.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 04/01/2018
ms.custom: mvc
ms.openlocfilehash: daa7ea345abb6228bee2d1ca5bfcc3850aaff9c3
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="quickstart-create-an-azure-database-for-postgresql-using-the-azure-cli"></a>Início Rápido: criar um Banco de Dados do Azure para PostgreSQL usando a CLI do Azure
O Banco de Dados do Azure para PostgreSQL é um serviço gerenciado que permite executar, gerenciar e dimensionar os bancos de dados altamente disponíveis do PostgreSQL na nuvem. A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts. Este início rápido mostra como criar um Banco de Dados do Azure para o servidor PostgreSQL em um [grupo de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) usando a CLI do Azure.

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este artigo exigirá que seja executada a CLI do Azure versão 2.0 ou posterior. Para ver a versão instalada, execute o comando `az --version`. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli). 

Se você estiver executando a CLI localmente, precisará fazer logon em sua conta usando o comando [az login](/cli/azure/authenticate-azure-cli?view=interactive-log-in). Observe a propriedade **id** da saída do comando para o nome da assinatura correspondente.
```azurecli-interactive
az login
```

Se tiver várias assinaturas, escolha a que for adequada para cobrança do recurso. Selecione a ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#az_account_set). Substitua a propriedade **id** da saída **logon az** para a sua assinatura no espaço reservado da ID da assinatura.
```azurecli-interactive
az account set --subscription <subscription id>
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando o comando [az group create](/cli/azure/group#az_group_create). Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo. Você deve fornecer um nome exclusivo. O exemplo a seguir cria um grupo de recursos denominado `myresourcegroup` no local `westus`.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Criar um Banco de Dados do Azure para o servidor PostgreSQL

Crie um [Banco de Dados do Azure para PostgreSQL](overview.md) usando o comando [az postgres server create](/cli/azure/postgres/server#az_postgres_server_create). Um servidor contém um grupo de bancos de dados gerenciados conjuntamente. 

O exemplo a seguir cria um servidor no Oeste dos EUA chamado `mydemoserver` em seu grupo de recursos `myresourcegroup` com o logon de administrador de servidor `myadmin`. Este é um servidor **Gen 4** de **Uso geral** com 2 **vCores**. O nome de um servidor é mapeado para o nome DNS e, portanto, deve ser globalmente exclusivo no Azure. Substitua o `<server_admin_password>` com seu próprio valor.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mydemoserver  --location westus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen4_2 --version 9.6
```

> [!IMPORTANT]
> O logon de administrador do servidor e a senha que você especificar aqui são necessários para fazer logon no servidor e em seus bancos de dados mais tarde neste Guia de início rápido. Lembre-se ou registre essas informações para o uso posterior.

Por padrão, o banco de dados **postgres** é criado em seu servidor. O [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) é um banco de dados padrão destinado a uso por usuários, utilitários e aplicativos de terceiros. 


## <a name="configure-a-server-level-firewall-rule"></a>Configurar uma regra de firewall no nível de servidor

Crie uma regra de firewall no nível de servidor do PostgreSQL do Azure com o comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#az_postgres_server_firewall_rule_create). Uma regra de firewall de nível de servidor permite que um aplicativo externo, tal como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/), conecte-se ao servidor por meio do firewall do serviço Azure PostgreSQL. 

Você pode definir uma regra de firewall que abranja um intervalo de IP aos quais você possa se conectar de sua rede. O exemplo a seguir usa [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#az_postgres_server_firewall_rule_create) para criar uma regra de firewall `AllowAllIps` para um intervalo de endereços IP. Para abrir todos os endereços IP, use 0.0.0.0 como o endereço IP inicial e 255.255.255.255 como o endereço final.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> O servidor PostgreSQL do Azure se comunica pela porta 5432. Ao se conectar de dentro de uma rede corporativa, o tráfego de saída pela porta 5432 talvez não seja permitido pelo firewall de sua rede. Solicite que seu departamento de TI abra a porta 5432 para se conectar ao seu servidor PostgreSQL do Azure.

## <a name="get-the-connection-information"></a>Obter informações de conexão

Para se conectar ao servidor, é preciso fornecer credenciais de acesso e informações do host.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mydemoserver
```

O resultado está no formato JSON. Anote o **administratorLogin** e o **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "myadmin",
  "earliestRestoreDate": null,
  "fullyQualifiedDomainName": "mydemoserver.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mydemoserver",
  "location": "westus",
  "name": "mydemoserver",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 2,
    "family": "Gen4",
    "name": "GP_Gen4_2",
    "size": null,
    "tier": "GeneralPurpose"
  },
  "sslEnforcement": "Enabled",
  "storageProfile": {
    "backupRetentionDays": 7,
    "geoRedundantBackup": "Disabled",
    "storageMb": 5120
  },
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-to-postgresql-database-using-psql"></a>Conectar-se ao banco de dados PostgreSQL usando psql

Se o computador cliente tiver o PostgreSQL instalado, você poderá usar uma instância local do [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) para se conectar a um servidor PostgreSQL do Azure. Usaremos agora o utilitário de linha de comando psql para nos conectarmos ao servidor PostgreSQL do Azure.

1. Execute o comando psql a seguir para se conectar a um Banco de Dados do Azure para servidor PostgreSQL
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Por exemplo, o comando a seguir se conecta ao banco de dados padrão chamado **postgres** no seu servidor PostgreSQL **mydemoserver.postgres.database.azure.com** usando as credenciais de acesso. Insira o `<server_admin_password>` que você escolheu quando uma senha foi solicitada a você.
  
  ```azurecli-interactive
psql --host=mydemoserver.postgres.database.azure.com --port=5432 --username=myadmin@mydemoserver --dbname=postgres
```

2.  Quando já estiver conectado ao servidor, crie um banco de dados em branco no prompt.
```sql
CREATE DATABASE mypgsqldb;
```

3.  No prompt, execute o seguinte comando para mudar a conexão para o banco de dados **mypgsqldb** recém-criado:
```sql
\c mypgsqldb
```

## <a name="connect-to-the-postgresql-server-using-pgadmin"></a>Conectar-se ao Servidor PostgreSQL usando pgAdmin

pgAdmin é uma ferramenta de software livre usada com PostgreSQL. Instale o pgAdmin por meio do [site do pgAdmin](http://www.pgadmin.org/). A versão de pgAdmin que você está usando pode ser diferente da que é usada neste Início Rápido. Leia a documentação de pgAdmin se precisar de orientação adicional.

1. Abra o aplicativo pgAdmin no computador cliente.

2. Na barra de ferramentas, vá para **Objeto**, passe o mouse sobre **Criar** e selecione **Servidor**.

3. Na caixa de diálogo **Criar – Servidor**, na guia **Geral**, insira um nome amigável exclusivo para o servidor, como **mydemoserver**.

   ![A guia “Geral”](./media/quickstart-create-server-database-azure-cli/9-pgadmin-create-server.png)

4. Na caixa de diálogo **Criar - Servidor** da guia **Conexão**, preencha a tabela de configurações.

   ![A guia “Conexão”](./media/quickstart-create-server-database-azure-cli/10-pgadmin-create-server.png)

    parâmetro pgAdmin |Valor|DESCRIÇÃO
    ---|---|---
    Nome/endereço do host | Nome do servidor | O valor do nome do servidor usado ao criar o Banco de Dados do Azure para o servidor PostgreSQL anteriormente. Nosso servidor de exemplo é **mydemoserver.postgres.database.azure.com.** Use o nome de domínio totalmente qualificado (**\*.postgres.database.azure.com**), conforme mostrado no exemplo. Caso não se lembre do nome do servidor, siga as etapas da seção anterior para obter as informações de conexão. 
    Porta | 5432 | A porta a ser usada ao se conectar ao Banco de Dados do Azure para o servidor PostgreSQL. 
    Banco de dados de manutenção | *postgres* | O nome do banco de dados padrão gerado pelo sistema.
    Nome de Usuário | Nome de logon do administrador do servidor | O nome de usuário de logon do administrador do servidor fornecido ao criar o Banco de Dados do Azure para o servidor PostgreSQL anteriormente. Caso não se lembre do nome de usuário, siga as etapas da seção anterior para obter as informações de conexão. O formato é *username@servername*.
    Senha | Sua senha de administrador | A senha que você escolheu ao criar o servidor anteriormente neste Guia de início rápido.
    Função | Deixar em branco | Não é necessário fornecer um nome de função neste momento. Deixe o campo em branco.
    Modo SSL | *Exigir* | Você pode definir o modo SSL na guia SSL do pgAdmin. Por padrão, todos os Bancos de Dados do Azure para servidores PostgreSQL são criados com a imposição de SSL ligada. Para desligar a imposição de SSL, confira [Imposição de SSL](./concepts-ssl-connection-security.md).
    
5. Selecione **Salvar**.

6. No painel **Navegador** à esquerda, expanda o nó **Servidores**. Selecione o servidor, por exemplo, **mydemoserver**. Clique nele para se conectar a ele.

7. Expanda o nó do servidor e expanda **Bancos de Dados** nele. A lista deve conter o banco de dados *postgres* existente e outros bancos de dados criados. Você pode criar vários bancos de dados por servidor com o Banco de Dados do Azure para PostgreSQL.

8. Clique com o botão direito do mouse em **Bancos de Dados**, escolha o menu **Criar** e, em seguida, selecione **Banco de Dados**.

9. Digite um nome de banco de dados de sua escolha no campo **Banco de Dados**, como **mypgsqldb2**.

10. Selecione o **Proprietário** do banco de dados na caixa de listagem. Escolha o nome de logon do administrador do servidor, como o exemplo, **myadmin**.

   ![Criar um banco de dados em pgadmin](./media/quickstart-create-server-database-azure-cli/11-pgadmin-database.png)

11. Selecione **Salvar** para criar um novo banco de dados em branco.

12. No painel **Procurar**, veja o banco de dados criado na lista de bancos de dados com o nome do servidor.




## <a name="clean-up-resources"></a>Limpar recursos

Limpe todos os recursos que você criou no início rápido, excluindo o [Grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Outros inícios rápidos nessa coleção aproveitam esse início rápido. Se você planeja continuar trabalhando com os inícios rápidos subsequentes, não limpe os recursos criados neste início rápido. Se não planeja continuar, siga estas etapas para excluir todos os recursos criados por esse início rápido na CLI do Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Se você quiser simplesmente excluir o servidor recém-criado, poderá executar o comando [az postgres server delete](/cli/azure/postgres/server#az_postgres_server_delete).
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mydemoserver
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)

