---
title: 'Tutorial: integração do Azure Active Directory ao Dynamic Signal | Microsoft Docs'
description: Saiba como configurar o logon único entre o Microsoft Azure Active Directory e o Dynamic Signal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 863f7340-b065-4f59-b092-daa67da6f703
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2018
ms.author: jeedes
ms.openlocfilehash: 48ea33c2542abfc318a326556aa0c47f568e3335
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-azure-active-directory-integration-with-dynamic-signal"></a>Tutorial: integração do Azure Active Directory ao Dynamic Signal

Neste tutorial, você aprende a integrar o Dynamic Signal ao Azure AD (Azure Active Directory).

A integração do Dynamic Signal ao Microsoft Azure Active Directory oferece os seguintes benefícios:

- No Microsoft Azure Active Directory, você poderá controlar quem tem acesso ao Dynamic Signal.
- Você pode permitir que seus usuários façam logon automaticamente no Dynamic Signal (logon único) com as contas do Microsoft Azure Active Directory deles.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>pré-requisitos

Para configurar a integração do Microsoft Azure Active Directory ao Dynamic Signal, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Dynamic Signal

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar Dynamic Signal pela Galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-dynamic-signal-from-the-gallery"></a>Adicionar Dynamic Signal pela Galeria
Para configurar a integração do Dynamic Signal ao Microsoft Azure Active Directory, você precisará adicionar o Dynamic Signal da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Dynamic Signal da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

4. Na caixa de pesquisa, digite **Dynamic Signal**, selecione **Dynamic Signal** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Dynamic Signal na lista de resultados](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Microsoft Azure Active Directory com o Dynamic Signal, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Microsoft Azure Active Directory precisa saber qual usuário do Dynamic Signal é equivalente a um usuário do Microsoft Azure Active Directory. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Microsoft Azure Active Directory e o usuário relacionado no Dynamic Signal.

Para configurar e testar o logon único do Microsoft Azure Active Directory com o Dynamic Signal, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Dynamic Signal](#create-a-dynamic-signal-test-user)** – para ter um equivalente de Brenda Fernandes no Dynamic Signal vinculado à representação do usuário no Microsoft Azure Active Directory.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Microsoft Azure Active Directory no Portal do Azure e configurará o logon único no aplicativo Dynamic Signal.

**Para configurar o logon único do Microsoft Azure Active Directory com o Dynamic Signal, realize as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos **Dynamic Signal**, clique em **Logon único**.

    ![Link Configurar logon único][4]

2. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_samlbase.png)

3. Na seção **Domínio e URLs do Dynamic Signal**, execute as seguintes etapas:
 
    ![Informações de logon único de Domínio e URLs do Dynamic Signal](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.voicestorm.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.voicestorm.com`

    c. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.voicestorm.com/User/SsoResponse`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada. Contate a [equipe de suporte ao cliente do Dynamic Signal](mailto:support@dynamicsignal.com) para obter esses valores. 

4. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_certificate.png) 

5. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_400.png)
    
6. Na seção **Configuração do Dynamic Signal**, clique em **Configurar Dynamic Signal** para abrir a janela **Configurar logon**. Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**

    ![Configuração do Dynamic Signal](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_configure.png) 

7. Para configurar o logon único no lado do **Dynamic Signal**, é necessário enviar o **Certificado (Base64) baixado, a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** para a [equipe de suporte do Dynamic Signal](mailto:support@dynamicsignal.com). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/active-directory-saas-dynamicsignal-tutorial/create_aaduser_01.png)

2. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-dynamicsignal-tutorial/create_aaduser_02.png)

3. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/active-directory-saas-dynamicsignal-tutorial/create_aaduser_03.png)

4. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/active-directory-saas-dynamicsignal-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-dynamic-signal-test-user"></a>Criar um usuário de teste do Dynamic Signal

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Dynamic Signal. O Dynamic Signal dá suporte ao provisionamento just-in-time, que está habilitado por padrão. Não há itens de ação para você nesta seção. Um novo usuário é criado durante uma tentativa de acessar o Dynamic Signal, caso ele ainda não exista.

>[!Note]
>Se você precisar criar um usuário manualmente, contate a [equipe de suporte do Dynamic Signal](mailto:support@dynamicsignal.com).

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Dynamic Signal.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Dynamic Signal, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

2. Na lista de aplicativos, escolha **Dynamic Signal**.

    ![O link do Dynamic Signal na lista Aplicativos](./media/active-directory-saas-dynamicsignal-tutorial/tutorial_dynamicsignal_app.png)  

3. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

4. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

5. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

6. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

7. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Dynamic Signal no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do Dynamic Signal.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dynamicsignal-tutorial/tutorial_general_203.png

