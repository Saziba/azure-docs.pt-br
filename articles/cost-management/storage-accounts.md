---
title: Configurar contas de armazenamento para o Gerenciamento de Custos do Azure | Microsoft Docs
description: Este artigo descreve como configurar contas de armazenamento do Azure e classificações de armazenamento AWS para Gerenciamento de Custos do Azure.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 04/26/2018
ms.topic: conceptual
ms.service: cost-management
manager: carmonm
ms.custom: ''
ms.openlocfilehash: 76a9fc586a1932b8b5e664b6c964f0c7d3eac4d4
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="configure-storage-accounts-for-cost-management"></a>Configurar contas de armazenamento para Gerenciamento de Custos

<!--- intent: As a Cost Management user, I want to configure Cost Management to use my cloud service provider storage account to store my reports. -->

Você pode salvar relatórios de gerenciamento de custo no portal de Cloudyn, armazenamento do Azure ou AWS buckets de armazenamento. Salvar seus relatórios no portal de Cloudyn é gratuito. No entanto, salvar seus relatórios para o armazenamento de seu provedor serviço de nuvem é opcional e incorre em custos adicionais. Este artigo o ajudará a configurar contas de armazenamento do Azure e buckets de armazenamento Amazon Web Services (AWS) para armazenar seus relatórios.

## <a name="prerequisites"></a>pré-requisitos

Você deve ter uma conta de armazenamento do Azure ou uma bucket de armazenamento da Amazon.

Se você não tiver uma conta de armazenamento do Azure, você precisa criar uma. Para saber mais sobre como criar uma nova conta de armazenamento, confira [Criar uma nova conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).

Se você não tiver um bucket de serviço de armazenamento AWS (S3), você precisa criar um. Para saber mais sobre como criar um bucket S3, confira [Criar um Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).

## <a name="configure-your-azure-storage-account"></a>Configure sua conta de armazenamento do Azure

Configurar o armazenamento do Azure para uso pelo Gerenciamento de Custo é simples. Obtenha detalhes sobre a conta de armazenamento e copie-os no portal de Cloudyn.

1. Faça logon no Portal do Azure em http://portal.azure.com.
2. Clique em **Todos os Serviços**, selecione **contas de Armazenamento**, role para a conta de armazenamento que você deseja usar e, em seguida, selecione a conta.
3. No menu da sua conta de armazenamento em **Configurações**, escolha **Chaves de acesso**.
4. Copie o **nome da conta de armazenamento** e a **cadeia de caracteres de Conexão** em key1.  
![Chaves de acesso de armazenamento do Azure](./media/storage-accounts/azure-storage-access-keys.png)  
5. Abra o portal da Cloudyn no portal do Azure ou navegue até https://azure.cloudyn.com e faça login.
6. Clique no símbolo de engrenagem e, em seguida, selecione **Gerenciamento de Armazenamento de Relatórios**.
7. Clique em **Adicionar novo +** e certifique-se de que o Microsoft Azure está selecionado. Cole o nome da conta de armazenamento do Azure na área **Nome**. Colar a **cadeia de caracteres de conexão** na área de trabalho correspondente. Insira um nome de contêiner e então clique em **Salvar**.  
![Armazenamento Cloudyn configurado para o Azure](./media/storage-accounts/azure-cloudyn-storage.png)

  Sua nova entrada de armazenamento do relatório do Azure aparece na lista de contas de armazenamento.  
    ![Novo armazenamento de relatório do Azure, na lista](./media/storage-accounts/azure-storage-entry.png)


Você pode agora salvar relatórios no armazenamento do Azure. Ao exibir qualquer relatório, clique em **Ações** e, em seguida, selecione **Agendar relatório**. Nomeie o relatório e em seguida ou adicione sua própria URL ou use uma URL criada automaticamente. Selecione **Salvar no armazenamento** e, em seguida, selecione a conta de armazenamento. Digite um prefixo que seja anexado ao nome do arquivo do relatório. Selecione um formato de arquivo CSV ou JSON e, em seguida, salve o relatório.

## <a name="configure-an-aws-storage-bucket"></a>Configurar uma bucket de armazenamento AWS

O Cloudyn usa as credenciais existentes do AWS: usuário ou função, para salvar os relatórios para o bucket. Para testar o acesso, Cloudyn tenta salvar um pequeno arquivo de texto para o bucket com o nome do arquivo _check-bucket-permission.txt_.

Forneça o Cloudyn função ou o usuário com a permissão PutObject para o bucket. Em seguida, use um bucket existente ou crie um novo para salvar relatórios. Finalmente, decida como gerenciar a classe de armazenamento, definir regras de ciclo de vida ou remova arquivos desnecessários.

###  <a name="assign-permissions-to-your-aws-user-or-role"></a>Atribuir permissões para o usuário AWS ou função

Quando você cria uma nova política, você pode fornecer as permissões exatas necessárias para salvar um relatório em um bucket S3.

1. Entrar no console do AWS e selecione **serviços**.
2. Na lista de serviços, selecione **IAM**.
3. Selecione **Políticas** no lado esquerdo do console e, em seguida, clique **Criar política**.
4. Clique na guia **JSON**.
5. A seguinte política permite que você salve um relatório em um bucket S3. Copie e cole o seguinte exemplo de política para a guia **JSON**. Substitua &lt;bucketname&gt; com seu nome de bucket.

  ```
{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid":  "CloudynSaveReport2S3",
        "Effect":      "Allow",
        "Action": [
          "s3:PutObject"
        ],
        "Resource": [
          "arn:aws:s3:::<bucketname>/*"
        ]
      }
    ]
}
```

6. Clique em **Revisar política**.  
    ![Revisar política](./media/storage-accounts/aws-policy.png)  
7. Na página de política de análise, digite um nome para a política. Por exemplo, _CloudynSaveReport2S3_.
8. Clique **Criar política**.

### <a name="attach-the-policy-to-a-cloudyn-role-or-user-in-your-account"></a>Anexar a política para uma função de Cloudyn ou um usuário em sua conta

Para anexar a nova política, você abre o console do AWS e edita função Cloudyn ou do usuário.

1. Entre no console do AWS e selecione **serviços**, em seguida, selecione **IAM** da lista de serviços.
2. Selecione **funções** ou **usuários** do lado esquerdo do console.

**Para funções:**

  1. Clique no nome da função Cloudyn.
  2. Na guia **Permissões**, clique em **Adicionar**.
  3. Pesquise a política que você criou e selecione-a e, então clique em **Anexar Política**.
    ![AWS - anexar política para uma função](./media/storage-accounts/aws-attach-policy-role.png)

**Para usuários:**

1. Selecione o usuário Cloudyn.
2. Na guia **Permissões**, clique em **Adicionar permissões**.
3. Na seção **Conceder Permissões**, selecione **Anexar políticas existentes diretamente**.
4. Pesquise a política que você criou e selecione-a e, então clique em **Próximo: Revisar**.
5. Em adicionar permissões à página de nome de função, clique em **adicionar permissões**.  
    ![AWS - anexar Política para um usuário](./media/storage-accounts/aws-attach-policy-user.png)


### <a name="optional-set-permission-with-bucket-policy"></a>Opcional: Definir permissão com a política de bucket

Você também pode definir permissão para criar relatórios sobre o bucket S3 usando uma política de bucket. No modo de exibição clássico da S3:

1. Crie ou selecione um bucket existente.
2. Clique na guia **Permissões** e, em seguida, clique em **política de bucket**.
3. Copie e cole o seguinte exemplo de política. Substitua &lt;bucket\_nome&gt; e &lt;Cloudyn\_princípio&gt; com ARN da sua partição. Substitua o ARN da função ou usuário usado pelo Cloudyn.

  ```
{
  "Id": "Policy1485775646248",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SaveReport2S3",
      "Action": [
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": "<bucket_name>/*",
      "Principal": {
        "AWS": [
          "<Cloudyn_principle>"
        ]
      }
    }
  ]
}
```

4. No editor de política de Bucket, clique em **salvar**.

### <a name="add-aws-report-storage-to-cloudyn"></a>Adicionar armazenamento de relatório AWS Cloudyn

1. Abra o portal da Cloudyn no portal do Azure ou navegue até https://azure.cloudyn.com e faça login.
2. Clique no símbolo de engrenagem e, em seguida, selecione **Gerenciamento de Armazenamento de Relatórios**.
3. Clique em **Adicionar novo +** e certifique-se de que o AWS está selecionado.
4. Selecione um bucket de armazenamento e de conta. O nome da partição de armazenamento AWS é preenchido automaticamente.  
    ![Adicionar armazenamento de relatório para o bucket AWS](./media/storage-accounts/aws-cloudyn-storage.png)  
5. Clique em **Salvar**, em seguida, clique em **Ok**.

    Sua nova entrada de armazenamento do relatório do AWS aparece na lista de contas de armazenamento.  
    ![Novo armazenamento de relatório do AWS na lista](./media/storage-accounts/aws-storage-entry.png)


Você pode agora salvar relatórios no armazenamento do Azure. Ao exibir qualquer relatório, clique em **Ações** e, em seguida, selecione **Agendar relatório**. Nomeie o relatório e em seguida ou adicione sua própria URL ou use uma URL criada automaticamente. Selecione **Salvar no armazenamento** e, em seguida, selecione a conta de armazenamento. Digite um prefixo que seja anexado ao nome do arquivo do relatório. Selecione um formato de arquivo CSV ou JSON e, em seguida, salve o relatório.

## <a name="next-steps"></a>Próximas etapas

- Revise [Entendendo sobre relatórios de gerenciamento de custo](understanding-cost-reports.md) para saber mais sobre as funções de relatórios de gerenciamento de custo e a estrutura básica.
