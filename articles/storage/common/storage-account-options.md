---
title: Opções de conta do Armazenamento do Azure | Microsoft Docs
description: Noções básicas sobre opções para uso do Armazenamento do Azure.
services: storage
author: jirwin
manager: jwillis
ms.service: storage
ms.workload: storage
ms.topic: get-started-article
ms.date: 01/17/2018
ms.author: jirwin
ms.openlocfilehash: 75d1580df5e36b2c88939fde9077c5a1948f6348
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="azure-storage-account-options"></a>Opções da conta de Armazenamento do Azure

## <a name="overview"></a>Visão geral
O Armazenamento do Azure fornece três opções de conta com diferentes preços e suporte a recursos. Considere essas diferenças antes de criar uma conta de armazenamento para determinar a melhor opção para seus aplicativos. As três opções de conta de armazenamento são:

* Contas de **GPv2 (Uso geral v2)** 
* Contas para **Uso geral v1 (GPv1)**
* Contas de **Armazenamento de Blobs**

Cada tipo de conta é descrito mais detalhadamente na seção a seguir:

## <a name="storage-account-options"></a>Opções da conta de armazenamento

### <a name="general-purpose-v2"></a>Uso geral v2

Contas de GPv2 são contas de armazenamento que dão suporte a todos os recursos mais recentes de arquivos, blobs, filas e tabelas. Essas contas aceitam as APIs e os recursos compatíveis com as contas de armazenamento de GPv1 e Blobs. Elas também oferecem os mesmos recursos de durabilidade, disponibilidade, escalabilidade e desempenho desses outros tipos de conta. As contas de GPv2 apresentam o melhor custo-benefício (menor preço por gigabyte) e valores de transação competitivos no setor.

Você pode atualizar sua conta de GPv1 para uma conta de GPv2 usando o PowerShell ou a CLI do Azure. 

Para blobs de bloco em uma conta de armazenamento GPv2, você pode escolher entre as camadas de armazenamento Frequente e Esporádica no nível de conta ou as camadas Frequente, Esporádica ou de Arquivos no nível de blob com base nos padrões de acesso. Armazene dados acessados frequentemente, com pouca frequência e raramente nas camadas de armazenamento frequente, esporádico e de arquivo respectivamente para otimizar os custos. 

As contas de Armazenamento GPv2 expõem o atributo **Camada de Acesso** no nível da conta, o qual especifica a camada de conta de armazenamento padrão como **Frequente** ou **Esporádica**. A camada de conta de armazenamento padrão é aplicada a qualquer blob que não tenha uma camada explícita definida no nível do blob. Se houver uma alteração no padrão de uso dos dados, você também poderá alternar entre as camadas de armazenamento a qualquer momento. A **camada de arquivo** só pode ser aplicada no nível do blob.

> [!NOTE]
> A alteração da camada de armazenamento pode resultar em cobranças adicionais. Para obter mais informações, confira a seção [Preços e cobrança](#pricing-and-billing).
>
> Na maioria dos cenários, a Microsoft recomenda o uso de contas de armazenamento de uso geral v2, em vez de contas de armazenamento de Blobs.

### <a name="upgrade-a-storage-account-to-gpv2"></a>Como atualizar uma conta de armazenamento para GPv2

Os usuários podem atualizar uma conta de GPv1 para uma conta de GPv2 a qualquer momento usando o PowerShell ou a CLI do Azure. Essa alteração não pode ser revertida, e nenhuma outra alteração é permitida.

#### <a name="upgrade-with-powershell"></a>Atualização com o PowerShell

Para atualizar uma conta GPv1 para uma conta de GPv2 usando o PowerShell, primeiro atualize o PowerShell para usar a versão mais recente do módulo **AzureRm.Storage**. Acesse [Como instalar e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) para obter informações sobre como instalar o PowerShell. Em seguida, chame o comando a seguir para atualizar a conta, substituindo o nome do seu grupo de recursos e a conta de armazenamento:

```powershell
Set-AzureRmStorageAccount -ResourceGroupName <resource-group> -AccountName <storage-account> -UpgradeToStorageV2
```

#### <a name="upgrade-with-azure-cli"></a>Atualização com a CLI do Azure

Para atualizar uma conta GPv1 para uma conta de GPv2 usando a CLI do Azure, primeiro instale a versão mais recente da CLI do Azure. Para obter informações sobre como instalar a CLI 2.0 do Azure, veja [Como instalar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). Em seguida, chame o comando a seguir para atualizar a conta, substituindo o nome do seu grupo de recursos e a conta de armazenamento:

```cli
az storage account update -g <resource-group> -n <storage-account> --set kind=StorageV2
```` 

### <a name="general-purpose-v1"></a>Uso geral v1

As contas de Uso geral v1 (GPv1) fornecem o acesso a todos os Serviços de Armazenamento do Azure, mas talvez não tenham os recursos mais recentes ou o menor preço por gigabyte. Por exemplo, não há suporte para armazenamento esporádico e de arquivo na GPv1. O preço é inferior para transações GPv1, portanto, cargas de trabalho com alta rotatividade ou altas taxas de leitura podem se beneficiar desse tipo de conta.

As contas de armazenamento de Uso geral v1 (GPv1) são o tipo de conta de armazenamento mais antiga e a única que pode ser usada no modelo de implantação clássico. 

### <a name="blob-storage-accounts"></a>Contas de armazenamento de Blobs

Contas de Armazenamento de Blobs oferecem suporte a todos os mesmos recursos de blob de blocos como de GPv2, mas são limitadas a dar suporte apenas a Blobs de blocos. O preço é muito semelhante ao preço de contas para uso geral v2. Os clientes devem analisar as diferenças de preço entre contas de Armazenamento de Blobs e de GPv2 e considerar fazer upgrade para GPv2. Esse upgrade não pode ser desfeito.

A capacidade de atualizar as contas de armazenamento de Blobs para GPv2 estará disponível em breve.

> [!NOTE]
> As contas de armazenamento de blobs oferecem suporte apenas aos blobs de bloco e aos blobs de acréscimo, e não aos blobs de página.

## <a name="recommendations"></a>Recomendações

Veja [Sobre contas de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para saber mais informações sobre contas de armazenamento.

Para aplicativos que exigem apenas armazenamento de blobs de bloco ou acréscimo, é recomendável usar contas de armazenamento de GPv2 para aproveitar o modelo de preços diferenciado do armazenamento em camadas. No entanto, você talvez queira usar GPv1 em determinados cenários, como:

* Você ainda precisa usar o modelo de implantação clássico. As contas de armazenamento de Blobs só estão disponíveis por meio do modelo de implantação do Azure Resource Manager.

* Você usa grandes volumes de transações ou largura de banda de replicação geográfica, ambos custando mais em contas GPv2 e de armazenamento de Blobs que de GPv1 e não têm armazenamento suficiente que se beneficie da redução dos custos de armazenamento de GB.

* Você usa uma versão da [API REST dos Serviços de Armazenamento](https://msdn.microsoft.com/library/azure/dd894041.aspx) que é anterior a 2014-02-14 ou uma biblioteca de cliente com uma versão inferior a 4.x e não pode atualizar o aplicativo.

> [!NOTE]
> Contas de armazenamento de Blobs atualmente têm suporte em todas as regiões do Azure.

## <a name="pricing-and-billing"></a>Preços e cobrança
Todas as contas de armazenamento usam um modelo de preços para o armazenamento de blobs com base na camada de cada blob. Ao se usar uma conta de armazenamento, as seguintes considerações de cobranças são aplicáveis:

* **Custos de armazenamento**: além da quantidade de dados armazenados, o custo de armazenamento de dados varia de acordo com a camada de armazenamento. O custo por gigabyte diminui conforme a camada fica mais esporádica.

* **Custos de acesso a dados**: os encargos de acesso a dados aumentam conforme a camada fica mais esporádica. Para dados na camada de armazenamento esporádico e de arquivos, será cobrado um encargo de acesso a dados por gigabyte para leituras.

* **Custos de transações**: há um encargo por transação para todas as camadas que aumenta à medida que a camada fica mais esporádica.

* **Custos de transferência de dados de replicação geográfica**: isso só se aplica a contas com replicação geográfica configurada, incluindo GRS e RA-GRS. A transferência de dados de replicação geográfica acarreta um encargo por gigabyte.

* **Custos de transferência de dados de saída**: transferências de dados de saída (dados que são transferidos para fora de uma região do Azure) acarretam a cobrança por uso de largura de banda por gigabyte, de forma consistente com as contas de armazenamento de finalidade geral.

* **Alteração da camada de armazenamento**: A alteração da camada de armazenamento da conta de esporádico para frequente acarretará um encargo igual à leitura de todos os dados existentes na conta de armazenamento. No entanto, alterar a camada de armazenamento de conta de frequente para esporádico incorre em um custo igual à gravação de todos os dados na camada esporádica (apenas contas de GPv2).

> [!NOTE]
> Para saber mais informações sobre o modelo de preços para contas de Armazenamento de Blobs, confira a página [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/). Para saber mais informações sobre os encargos de transferência de dados de saída, confira a página [Detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="quickstart-scenarios"></a>Cenários de início rápido

Nesta seção, os cenários a seguir são demonstrados usando o Portal do Azure:

* Como criar uma conta de armazenamento de GPv2.
* Como converter uma conta GPv1 ou de armazenamento de blobs em uma conta de armazenamento de GPv2.
* Como definir a conta e a camada blobs em uma conta de armazenamento de GPv2.

Não é possível definir o nível de acesso para arquivo morto nos exemplos a seguir, porque essa configuração se aplica à conta de armazenamento inteira. Arquivo morto só pode ser definido em um blob específico.

### <a name="create-a-gpv2-storage-account-using-the-azure-portal"></a>Criar uma conta de armazenamento de GPv2 usando o portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com).

2. No menu Hub, selecione **Criar um recurso** > **Dados + Armazenamento** > **Conta de armazenamento**.

3. Insira um nome para a conta de armazenamento.

    Esse nome deve ser exclusivo globalmente; ele é usado como parte da URL utilizada para acessar os objetos na conta de armazenamento.  

4. Selecione **Gerenciador de Recursos** como o modelo de implantação.

    O armazenamento em camadas só pode ser usado com as contas de armazenamento do Resource Manager, que é o modelo de implantação recomendado para os novos recursos. Para saber mais informações, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).  

5. Na lista suspensa **Tipo de conta**, selecione **Uso geral v2**.

    Quando você seleciona GPv2, o nível de desempenho é definido para Standard. O armazenamento em camadas não está disponível com o nível de desempenho Premium.

6. Selecione a opção de replicação para a conta de armazenamento: **LRS**, **ZRS**, **GRS** ou **RA-GRS**. O padrão é **RA-GRS**.

    LRS = armazenamento com redundância local; ZRS = armazenamento com redundância de zona; GRS = armazenamento com redundância geográfica (duas regiões); RA-GRS é o armazenamento com redundância geográfica e acesso de leitura (duas regiões com acesso de leitura para o segundo).

    Para obter mais detalhes sobre as opções de replicação do Armazenamento do Azure, confira [Replicação do Armazenamento do Azure](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

7. Selecione a camada de armazenamento adequada para suas necessidades: defina a **Camada de acesso** como **Estática** ou **Dinâmica**. O padrão é **Dinâmica**.

8. Selecione a assinatura na qual você deseja criar a nova conta de armazenamento.

9. Especifique um novo grupo de recursos ou selecione um grupo de recursos existente. Para saber mais sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

10. Selecione a região de sua conta de armazenamento.

11. Clique em **Criar** para criar a conta de armazenamento.

### <a name="convert-a-gpv1-account-to-a-gpv2-storage-account-using-the-azure-portal"></a>Converter uma conta de GPv1 ou em uma conta de armazenamento de GPv2 usando o portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com).

2. Para navegar até sua conta de armazenamento, selecione **Todos os recursos** e selecione sua conta de armazenamento.

3. Na seção de Configurações, clique em **Configuração**.

4. Em **Tipo de conta**, clique em **Upgrade**.

5. Em **Confirmar upgrade**, digite o nome da sua conta. 

5. Clique em Upgrade na parte inferior da folha.

### <a name="change-the-storage-tier-of-a-gpv2-storage-account-using-the-azure-portal"></a>Alterar a camada de armazenamento em uma conta de armazenamento de GPv2 usando o portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com).

2. Para navegar até sua conta de armazenamento, selecione **Todos os recursos** e selecione sua conta de armazenamento.

3. Na folha Configurações, clique em **Configuração** para exibir e/ou alterar a configuração da conta.

4. Selecione a camada de armazenamento adequada para suas necessidades: defina a **Camada de acesso** como **Estática** ou **Dinâmica**.

5. Clique em Salvar na parte superior da folha.

### <a name="change-the-storage-tier-of-a-blob-using-the-azure-portal"></a>Alterar a camada de armazenamento de um blob usando o Portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com).

2. Para navegar até seu blob em sua conta de armazenamento, selecione **Todos os recursos**, selecione sua conta de armazenamento, selecione seu contêiner e depois seu blob.

3. Na folha de propriedades do Blob, clique no menu suspenso **Camada de Acesso** para selecionar a camada de armazenamento **Frequente**, **Esporádico**, ou **Arquivamo**.

5. Clique em Salvar na parte superior da folha.

> [!NOTE]
> A alteração da camada de armazenamento pode resultar em cobranças adicionais. Para obter mais informações, confira a seção [Preços e cobrança](#pricing-and-billing).


## <a name="evaluating-and-migrating-to-gpv2-storage-accounts"></a>Avaliando e migrando para contas de armazenamento de GPv2
O objetivo desta seção é ajudar os usuários a fazer uma transição tranquila para usar contas de armazenamento de GPv2 (em oposição a de GPv1). Há dois cenários de usuário:

* Você tem uma conta existente de armazenamento de GPv1 e deseja avaliar uma alteração para uma conta de armazenamento de GPv2 com a camada de armazenamento adequada.
* Você optou por usar uma conta de armazenamento de GPv2 ou já tem uma e deseja avaliar se deve usar a camada de armazenamento dinâmica ou estática.

Em ambos os casos, a prioridade é estimar o custo de armazenar e acessar os dados armazenados em uma conta de armazenamento de GPv2 e comparar isso com seus custos atuais.

## <a name="evaluating-gpv2-storage-account-tiers"></a>Avaliando camadas de conta de armazenamento de GPv2

Para estimar o custo de armazenar e acessar dados armazenados em uma conta de armazenamento de GPv2, você precisa avaliar seu padrão de uso existente ou estimar seu padrão de uso. Em geral, você precisa saber:

* Consumo de armazenamento: quanto dados são armazenados e como isso é alterado mensalmente?

* Padrão de acesso de armazenamento: quantos dados são lidos e gravados na conta (incluindo novos dados)? Quantas transações são usadas para acesso a dados e que tipo de transações são elas?

## <a name="monitoring-existing-storage-accounts"></a>Monitorando contas de armazenamento existentes

Para monitorar suas contas de armazenamento existentes e reunir esses dados, você poderá fazer uso da Análise de Armazenamento do Azure, que executa logs e fornece dados de métrica para uma conta de armazenamento. A Análise de Armazenamento pode armazenar métricas que incluem estatísticas de transação agregadas e dados de capacidade sobre solicitações em um serviço de armazenamento para tipos de conta de Armazenamento de GPv1, GPv2 e armazenamento de Blobs. Esses dados são armazenados em tabelas conhecidas na mesma conta de armazenamento.

Para obter mais detalhes, acesse [Sobre métricas de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343258.aspx) e [Esquema de tabela de métricas da análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> As contas de Armazenamento de Blobs expõem o ponto de extremidade de serviço de tabela apenas para armazenar e acessar dados de métricas dessa conta. 

Para monitorar o consumo do Armazenamento de Blobs, você precisa habilitar as métricas de capacidade.
Com esse recurso habilitado, os dados de capacidade são gravados diariamente para o serviço Blob de uma conta de armazenamento e registrados como uma entrada de tabela gravada na tabela *$MetricsCapacityBlob* dentro da mesma conta de armazenamento.

Para monitorar os padrões de acesso a dados para o armazenamento de Blobs, você precisa habilitar as métricas de transações por hora da API. Com esse recurso habilitado, as transações por API são agregadas a cada hora e registradas como uma entrada de tabela que é gravada na tabela *$MetricsHourPrimaryTransactionsBlob* dentro da mesma conta de armazenamento. A tabela *$MetricsHourSecondaryTransactionsBlob* registra as transações para o ponto de extremidade secundário ao usar contas de armazenamento RA-GRS.

> [!NOTE]
> Caso você tenha uma conta de armazenamento para uso geral na qual armazenou blobs de página, discos de máquina virtual, ou filas, arquivos ou tabelas junto com blob de bloco e de acréscimo, esse processo de previsão não se aplica. Isso ocorre porque os dados de capacidade não diferenciam blobs de bloco de outros tipos e não fornecem dados de capacidade para outros tipos de dados. Caso use esses tipos, uma metodologia alternativa é examinar as quantidades na sua conta mais recente.

Para obter uma boa aproximação do consumo de dados e do padrão de acesso, recomendamos escolher um período de retenção para as métricas que representam seu uso regular e extrapolar. Uma opção é manter os dados de métricas por sete dias e coletar os dados de cada semana, para analisá-las no final do mês. Outra opção é manter os dados de métricas dos últimos 30 dias e coletar e analisar os dados ao fim do período de 30 dias.

Para obter detalhes sobre como habilitar, coletar e exibir dados de métricas, consulte [Habilitando métricas do Armazenamento do Azure e exibindo dados de métricas](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

> [!NOTE]
> O armazenamento, acesso e download de dados de análise também serão cobrados, assim como os dados de usuário comuns.

### <a name="utilizing-usage-metrics-to-estimate-costs"></a>Utilizando métricas de uso para estimar custos

#### <a name="storage-costs"></a>Custos de armazenamento

A última entrada na tabela de métricas de capacidade *$MetricsCapacityBlob* com a chave de linha *'data'* mostra a capacidade de armazenamento consumida por dados do usuário. A última entrada na tabela de métricas de capacidade *$MetricsCapacityBlob* com a chave de linha *'analytics'* mostra a capacidade de armazenamento consumida por logs de análise.

Essa capacidade total consumida tanto por dados de usuário quanto logs de análise (se habilitado) pode ser usada para estimar o custo de armazenar dados na conta de armazenamento. O mesmo método também pode ser usado para estimar os custos de armazenamento nas contas de armazenamento de GPv1.

#### <a name="transaction-costs"></a>Custos de transação

A soma de *'TotalBillableRequests'* de todas as entradas para uma API na tabela de métricas de transação indica a quantidade total de transações para essa API em particular. *Por exemplo*, o número total de transações *'GetBlob'* em um determinado período pode ser calculado pela soma do total de solicitações faturáveis para todas as entradas com a chave de linha *'user;GetBlob'*.

Para estimar os custos de transação para contas de armazenamento de Blobs, você precisa dividir as transações em três grupos, já que elas possuem preços diferentes.

* Transações de gravação, como *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* e *'CopyBlob'*.
* Transações de exclusão, como *'DeleteBlob'* e *'DeleteContainer'*.
* Todas as outras transações.

Para estimar os custos de transação para contas de armazenamento de GPv1, você precisa agregar todas as transações, independentemente da operação/API.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Custos de transferência de dados de acesso aos dados e de replicação geográfica

Embora a análise de armazenamento não forneça a quantidade de dados lida e gravada em uma conta de armazenamento, ela pode ser estimada aproximadamente examinando a tabela de métricas de transação. A soma de *'TotalIngress'* de todas as entradas para uma API na tabela de métricas de transação indica a quantidade total de dados de entrada em bytes para essa API em particular. Da mesma forma, a soma de *'TotalEgress'* indica a quantidade total de dados de saída, em bytes.

Para estimar os custos de acesso de dados para as contas de armazenamento de Blobs, você precisa dividir as transações em dois grupos.

* A quantidade de dados recuperados da conta de armazenamento pode ser estimada observando a soma de *'TotalEgress'* basicamente para as operações *'GetBlob'* e *'CopyBlob'*.

* A quantidade de dados gravados na conta de armazenamento pode ser estimada observando a soma de *'TotalIngress'* basicamente para as operações *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* e *'AppendBlock'*.

O custo da transferência de dados de replicação geográfica para contas de armazenamento de Blobs também pode ser calculado usando a estimativa de quantidade de dados gravados ao usar uma conta de armazenamento GRS ou RA-GRS.

> [!NOTE]
> Para obter um exemplo mais detalhado de como calcular os custos para usar a camada de armazenamento quente ou fria, dê uma olhada nas Perguntas frequentes intituladas *“O que são as camadas de acesso quente e fria e como devo determinar qual delas usar?”* na [Página de preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).

## <a name="migrating-existing-data"></a>Migração de dados existentes

Uma conta de GPv1 pode ser facilmente atualizada para GPv2 sem tempo de inatividade ou alterações na API e sem a necessidade de movimentar dados. Por esse motivo, é recomendável que você migre contas GPv1 para contas GPv2, em vez de migrar para contas de armazenamento de Blobs.

No entanto, caso precise migrar para uma conta de Armazenamento de Blobs, você pode usar as instruções abaixo.

Uma conta de Armazenamento de Blobs é especializada no armazenamento exclusivo de blobs de bloco e de acréscimo. As contas de armazenamento de uso geral existentes, que permitem o armazenamento de tabelas, filas, arquivos e discos não podem ser convertidas em contas de Armazenamento de Blobs. Para usar as camadas de armazenamento, é necessário criar novas contas de Armazenamento de Blobs e migrar os dados existentes para as contas recém-criadas.

Você pode usar os métodos a seguir para migrar os dados existentes para as contas de armazenamento de Blobs a partir dos dispositivos de armazenamento locais, provedores de armazenamento de nuvem de terceiros ou de suas contas de armazenamento geral existentes no Azure:

### <a name="azcopy"></a>AzCopy

O AzCopy é um utilitário de linha de comando do Windows desenvolvido para cópia de dados de alto desempenho para dentro e para fora do Armazenamento do Azure. Você pode usar o AzCopy para copiar dados para sua conta de armazenamento de Blobs de suas contas de armazenamento de finalidade geral existentes ou carregar dados do dispositivo de armazenamento local para sua conta de armazenamento de Blobs.

Para obter mais informações, consulte [Transferir dados com o Utilitário de Linha de Comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Biblioteca de movimentação de dados

A biblioteca de movimentação de dados do Armazenamento do Azure para .NET baseia-se no framework de movimentação de dados de núcleo que habilita o AzCopy. A biblioteca foi projetada para operações de transferência de dados de alto desempenho, confiáveis e fáceis, de forma semelhante ao AzCopy. Isso permite que você aproveite todos os benefícios dos recursos fornecidos pelo AzCopy em seu aplicativo de forma nativa, sem a necessidade de lidar com a execução e o monitoramento de instâncias externas do AzCopy.

Para obter mais detalhes, veja [Biblioteca de Movimentação dos Dados do Armazenamento do Azure para .Net](https://github.com/Azure/azure-storage-net-data-movement)

### <a name="rest-api-or-client-library"></a>API REST ou biblioteca de cliente

Você pode criar um aplicativo personalizado para migrar os dados para uma conta de armazenamento de Blobs usando uma das bibliotecas de cliente do Azure ou a API REST dos serviços de armazenamento do Azure. O Armazenamento do Azure fornece bibliotecas de cliente avançadas para várias linguagens e plataformas, como .NET, Java, C++, Node.JS, PHP, Ruby e Python. As bibliotecas de cliente oferecem recursos avançados, como lógica de recuperação, registro em log e carregamentos paralelos. Você também pode desenvolver diretamente na API REST, que pode ser chamada por qualquer linguagem que faça solicitações HTTP/HTTPS.

Para saber mais informações, veja [Introdução ao Armazenamento de Blobs do Azure](../blobs/storage-dotnet-how-to-use-blobs.md).

> [!IMPORTANT]
> Blobs criptografados usando metadados relacionados à criptografia de armazenamento no lado do cliente com o blob. Se você copiar um blob que é criptografado com criptografia do lado do cliente, verifique se que a operação de cópia preserva os metadados de blob e especialmente os metadados relacionados à criptografia. Se você copiar um blob sem os metadados de criptografia, o conteúdo do blob não poderá ser recuperado novamente. Para obter mais detalhes sobre os metadados relacionados à criptografia, confira [Criptografia no Lado do Cliente do Armazenamento do Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="faq"></a>Perguntas frequentes

**As contas de armazenamento existentes ainda estão disponíveis?**

Sim, as contas de armazenamento existentes (GPv1) ainda estão disponíveis, e seus preços ou funcionalidade não foram alterados. As contas de GPv1 não têm a capacidade de escolher uma camada de armazenamento e não terão recursos de camadas no futuro.

**Por que e quando devo começar a usar contas de armazenamento de GPv2?**

Contas de armazenamento de GPv2 são especializadas em fornecer os mais baixos custos de armazenamento GB, oferecendo custos competitivos de transações e acesso de dados no setor. Futuramente, as contas de armazenamento de GPv2 serão a maneira recomendada para armazenar blobs, à medida que recursos futuros, como notificações de alteração forem introduzidos com base nesse tipo de conta. No entanto, você pode decidir quando deseja fazer upgrade com base nas necessidades de negócios. Por exemplo, você pode otimizar seus padrões de transação antes de fazer upgrade.

Não há suporte para fazer downgrade de GPv2, portanto, considere todas as implicações de preço antes de atualizar suas contas para GPv2.

**Posso fazer upgrade da minha conta de armazenamento existente para uma conta de armazenamento de GPv2?**

Sim. Contas de GPv1 podem ser atualizadas facilmente para GPv2 no portal ou usando o PowerShell ou a CLI. Contas de armazenamento de blobs podem ser atualizadas para GPv2 usando o PowerShell ou a CLI. A capacidade de atualizar uma conta de armazenamento de Blobs para GPv2 no portal estará disponível em breve.

Não há suporte para fazer downgrade de GPv2, portanto, considere todas as implicações de preço antes de atualizar suas contas para GPv2.

**Posso armazenar objetos em ambas as camadas de armazenamento na mesma conta?**

Sim. O atributo **Camada de Acesso** definido em um nível de conta é a camada padrão aplicada a todos os objetos na conta sem uma camada de conjunto explícita. No entanto, camadas no nível do blob permitem que você defina a camada de acesso no nível de objeto, independentemente da configuração de camada de acesso da conta. Os blobs em qualquer uma das três camadas de armazenamento (frequente, esporádica ou arquivo) podem existir na mesma conta.

**Posso alterar a camada de armazenamento da minha conta de armazenamento de GPv2?**

Sim, você pode alterar a camada de armazenamento de conta definindo o atributo **Access Tier** na conta de armazenamento. A alteração da camada de armazenamento é aplicada a todos os objetos armazenados na conta que não têm uma camada explícita definida. Alterar a camada de armazenamento de frequente para esporádico incorre em encargos (apenas para contas de armazenamento de GPv2) de operações de gravação (por 10.000), enquanto a alteração de esporádico para frequente incorre em encargos de operações de leitura (por 10.000) e de recuperação de dados (por GB) para leitura de todos os dados na conta.

**Com que frequência posso alterar a camada de armazenamento em minha conta de armazenamento de Blobs?**

Embora não imponhamos uma limitação à frequência com que a camada de armazenamento pode ser alterada, lembre-se de que a alteração da camada de armazenamento de estática para dinâmica incorrerá em encargos significativos. Não recomendamos alterar a camada de armazenamento com frequência.

**Os blobs na camada de armazenamento fria se comportam de forma diferente daqueles na camada de armazenamento quente?**

Os blobs na camada de armazenamento frequente das contas de Armazenamento de Blobs e de GPv2 têm a mesma latência que os blobs nas contas de armazenamento de GPv1. Os blobs na camada de armazenamento esporádica têm uma latência parecida (em milissegundos) que os blobs na camada frequente. Blobs na camada de armazenamento de arquivo têm várias horas de latência.

Os Blobs na camada de armazenamento fria têm um SLA (acordo de nível de serviço) com disponibilidade ligeiramente menor do que os blobs armazenados na camada de armazenamento quente. Para obter mais informações, veja [SLA para armazenamento](https://azure.microsoft.com/support/legal/sla/storage).

**Posso armazenar os blobs de página e discos de máquinas virtuais em contas de armazenamento de Blob?**

Nº As contas de armazenamento de blobs oferecem suporte apenas aos blobs de bloco e aos blobs de acréscimo, e não aos blobs de página. Os discos de máquina virtual do Azure têm o suporte de blobs de página e, como resultado, as contas de armazenamento de blobs não podem ser usadas para armazenar os discos da máquina virtual. No entanto, é possível armazenar backups dos discos de máquina virtual como blobs de bloco em uma conta de Armazenamento de Blobs. Esse é um dos motivos para considerar o uso de GPv2 em vez de contas de armazenamento de Blobs.

**Preciso alterar meus aplicativos existentes para usar contas de armazenamento de GPv2?**

Contas de armazenamento de GPv2 são 100% consistentes com a API com contas de Armazenamento de Blobs e de GPv1. Contanto que o aplicativo esteja usando blobs de bloco ou blobs de acréscimo e você esteja usando a versão 2014-02-14 da [API REST dos Serviços de Armazenamento](https://msdn.microsoft.com/library/azure/dd894041.aspx) ou mais recente, o aplicativo deverá funcionar. Se estiver usando uma versão mais antiga do protocolo, você precisa atualizar o aplicativo para usar a nova versão, para que funcione perfeitamente com os dois tipos de contas de armazenamento. Em geral, é sempre recomendável usar a última versão, independentemente do tipo de conta de armazenamento que você usa.

Os preços de GPv2 são geralmente maiores que de GPv1 para transações e largura de banda. Portanto, pode ser necessário otimizar seus padrões de transação antes de fazer a atualização, assim, sua fatura total não aumentará.

**Haverá uma alteração na experiência do usuário?**

As contas de armazenamento de GPv2 são bastante parecidas com as contas de armazenamento de GPv1 e oferecem suporte a todos os principais recursos do Armazenamento do Azure, incluindo alta durabilidade e disponibilidade, escalabilidade, desempenho e segurança. Além dos recursos e restrições específicos de contas de Armazenamento de Blobs e suas camadas de armazenamento, explicados acima, todo o resto permanece o mesmo ao fazer upgrade para o Armazenamento de Blobs ou de GPv2.

## <a name="next-steps"></a>Próximas etapas

### <a name="evaluate-blob-storage-accounts"></a>Avaliar as contas de armazenamento de Blobs

[Verificar a disponibilidade das contas de armazenamento de blobs por região](https://azure.microsoft.com/regions/#services)

[Avaliar o uso de suas contas de armazenamento atuais, habilitando as métricas do Armazenamento do Azure](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Verificar preços do armazenamento de blobs por região](https://azure.microsoft.com/pricing/details/storage/)

[Verificar os preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-gpv2-storage-accounts"></a>Começar a usar as contas de armazenamento de GPv2

[Introdução ao Armazenamento de Blobs do Azure](../blobs/storage-dotnet-how-to-use-blobs.md)

[Movendo dados para dentro e para fora do Armazenamento do Azure](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Transferir dados com o Utilitário da Linha de Comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Navegue e explore suas contas de armazenamento](http://storageexplorer.com/)
