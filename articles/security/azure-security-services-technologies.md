---
title: Tecnologias e serviços de segurança do Azure | Microsoft Docs
description: O artigo fornece uma lista estruturada das tecnologias e serviços de segurança do Azure.
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: a5a7f60a-97e2-49b4-a8c5-7c010ff27ef8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/26/2018
ms.author: barclayn
ms.openlocfilehash: eedfca2506f9e34b8e5039b0f101b1d4e68ef5a7
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="azure-security-services-and-technologies"></a>Tecnologias e serviços de segurança do Azure

Em nossas discussões com clientes do Azure atuais e futuros, frequentemente nos fazem a seguinte pergunta “você tem uma lista de todas as tecnologias e serviços relacionados à segurança que o Azure tem a oferecer?”

Ao avaliar as opções de provedor de serviços de nuvem, é útil ter essas informações.

A seguir está o nosso esforço inicial no fornecimento de uma lista. Ao longo do tempo, essa lista será alterada e aumentará, exatamente como o Azure. A lista é categorizada e a lista de categorias também aumentará ao longo do tempo. Lembre-se de visitar essa página regularmente para se manter atualizado sobre nossas tecnologias e serviços relacionados à segurança.

## <a name="azure-security---general"></a>Segurança do Azure: geral

* [Central de Segurança do Azure](https://azure.microsoft.com/documentation/services/security-center/)
* [Cofre da Chave do Azure](https://azure.microsoft.com/documentation/services/key-vault/)
* [Criptografia de Disco do Azure](azure-security-disk-encryption.md)
* [Log Analytics](../log-analytics/log-analytics-overview.md)
* [Azure Dev/Test Labs](https://azure.microsoft.com/documentation/services/devtest-lab/)

## <a name="azure-storage-security"></a>Segurança do Armazenamento do Azure

* [Criptografia do serviço de armazenamento do Azure](../storage/common/storage-service-encryption.md)
* [Armazenamento híbrido criptografado StorSimple](https://azure.microsoft.com/documentation/services/storsimple/)
* [Criptografia do lado do cliente do Azure](../storage/common/storage-client-side-encryption.md)
* [Assinaturas de Acesso Compartilhado do Armazenamento do Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Chaves de conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md)
* [Compartilhamentos de arquivos do Azure com criptografia SMB 3.0](../storage/files/storage-dotnet-how-to-use-files.md)
* [Análise do Armazenamento do Azure](https://msdn.microsoft.com/library/hh343270.aspx)

## <a name="azure-database-security"></a>Segurança de banco de dados do Azure

* [Firewall do SQL do Azure](../sql-database/sql-database-firewall-configure.md)
* [Criptografia de nível de célula do SQL do Azure](https://blogs.msdn.microsoft.com/sqlsecurity/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database/)
* [Criptografia de conexão do SQL do Azure](../sql-database/sql-database-control-access.md)
* [Autenticação do SQL do Azure](../sql-database/sql-database-control-access.md)
* [Criptografia sempre ativa do SQL do Azure](https://msdn.microsoft.com/library/mt163865.aspx)
* [Criptografia de nível de coluna do SQL do Azure](https://msdn.microsoft.com/library/ms179331.aspx)
* [Transparent Data Encryption do SQL do Azure](https://msdn.microsoft.com/library/dn948096.aspx)
* [Auditoria do Banco de Dados SQL do Azure](../sql-database/sql-database-auditing.md)

## <a name="azure-identity-and-access-management"></a>Gerenciamento de acesso e identidade do Azure

* [Controle de acesso baseado em função do Azure](../role-based-access-control/role-assignments-portal.md)
* [Active Directory do Azure](../active-directory/active-directory-whatis.md)
* [Active Directory B2C do Azure](../active-directory-b2c/active-directory-b2c-get-started.md)
* [Serviços de Domínio do Active Directory do Azure](../active-directory-domain-services/active-directory-ds-overview.md)
* [Autenticação Multifator do Azure](../active-directory/authentication/multi-factor-authentication.md)

## <a name="backup-and-disaster-recovery"></a>Backup e recuperação de desastre

* [Serviço de Backup do Azure](https://azure.microsoft.com/documentation/services/backup/)
* [Azure Site Recovery](https://azure.microsoft.com/documentation/services/site-recovery/)

## <a name="azure-networking"></a>Rede do Azure

* [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md)
* [Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Gateway de Aplicativo do Azure](../application-gateway/application-gateway-introduction.md)
* [Balanceador de carga do Azure](../load-balancer/load-balancer-overview.md)
* [Azure ExpressRoute](../expressroute/expressroute-introduction.md)
* [Gerenciador de Tráfego do Azure](../traffic-manager/traffic-manager-overview.md)
* [Proxy de aplicativo do Azure](../active-directory/active-directory-application-proxy-enable.md)
