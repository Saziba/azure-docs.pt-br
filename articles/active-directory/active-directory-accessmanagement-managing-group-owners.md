---
title: Próximas etapas para o gerenciamento de acesso usando grupos | Microsoft Docs
description: Método avançado para gerenciamento dos grupos de segurança e como usar esses grupos para gerenciar o acesso a um recurso.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/12/2017
ms.author: curtand
ms.custom: it-pro
ms.openlocfilehash: e4703ab5d9f4b8593e758764e50455672e368e18
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="managing-owners-for-a-group"></a>Gerenciando proprietários de um grupo
Após um proprietário de recurso ter o acesso a um grupo do Azure AD atribuído, a associação do grupo é gerenciada pelo proprietário do grupo. O proprietário do recurso delega efetivamente ao proprietário do grupo a permissão para atribuir usuários ao seu recurso.

## <a name="add-an-owner-to-a-group"></a>Adicionar um proprietário a um grupo

1. No [Centro de administração do Azure AD](https://aad.portal.azure.com), selecione **Usuários e grupos**.
2. Selecione **Todos os grupos** e, em seguida, abra o grupo ao qual você deseja adicionar os proprietários.
3. Selecione **Adicionar Proprietários**.
4. Na página **Adicionar proprietários**, selecione o usuário que deseja adicionar como o proprietário deste grupo e verifique se esse nome é adicionado ao painel **Selecionado**.

## <a name="remove-an-owner-from-a-group"></a>Remover um proprietário de um grupo

1. No [Centro de administração do Azure AD](https://aad.portal.azure.com), selecione **Usuários e grupos**.
2. Selecione **Todos os grupos** e, em seguida, abra o grupo do qual você deseja remover os proprietários.
3. Selecione a guia **Proprietários** .
4. Selecione o proprietário que você deseja remover deste grupo e, em seguida, selecione **Remover**.

## <a name="additional-information"></a>Informações adicionais
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciamento de acesso a recursos com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
