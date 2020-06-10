.. _setup:

<a name="laptop-setup-and-installation"></a>|laptop| Instalação e configuração
=================================

Bem-vindo ao workshop patrocinado do Azure para a PyCon 2020 (agora online)!

Esta seção orientará você pelos pré-requisitos do workshop.

Cada requisito é descrito aqui com instruções detalhadas sobre sua instalação.

<a name="python-3x"></a>Python 3.x
------------
Você deve ter uma das seguintes versões do Python instalada:

- 3.6
- 3.7
- 3.8

Essas são as versões compatíveis com o Azure Functions. Se você já tiver uma instalada, vá diretamente para o restante das instruções de configuração.

Caso contrário, você pode seguir este tutorial fantástico da `Real Python <https://realpython.com/installing-python/>`_ para obter uma instalação limpa do Python.

<a name="vs-code"></a>VS Code
--------

Usaremos o Visual Studio Code (também chamado de VS Code).
O VS Code é um IDE de software livre que pode ser facilmente estendido ou aprimorado com extensões.
Para este tutorial específico, usaremos as extensões do Python e das funções do Azure.
Para começar:

1. Baixe e instale o `VS Code <https://code.visualstudio.com//?WT.mc_id=?WT.mc_id=pycon_tutorial-github-taallard>`_ . Quando você for direcionado para a página de instalação, ela deverá identificar seu sistema operacional. Baixe o arquivo de instalação e siga as instruções.
2. Instale a `Python VS Code extension <https://marketplace.visualstudio.com/itemdetails?itemName=ms-python.python&wt.mc_id=?WT.mc_id=pycon_tutorial-github-taallard>`_ . Clique no botão Instalar no site da extensão. Isso iniciará o VS Code e solicitará sua confirmação para instalar.
3. Instale a `Azure Functions extension <https://marketplace.visualstudio.com/itemdetails?itemName=ms-azuretools.vscode-azurefunctions&wt.mc_id=?WT.mc_id=pycon_tutorial-github-taallard>`_

<a name="azure-account-and-credits"></a>Conta e créditos do Azure
---------------------------

Você pode se inscrever em sua conta do Azure e receber 12 meses de alguns serviços gratuitos, bem como US$ 200 em créditos.
Para começar a usar o Azure, acesse `this link <https://cda.ms/1fM>`_.

<a name="azure-cli-and-functions-core-tool"></a>Ferramenta básica de funções e CLI do Azure
----------------------------------
- Primeiro, precisamos instalar o CLI do Azure para poder implantar nossas funções

.. tabs::

  .. group-tab:: Mac OSX

    #. Install homebrew
    #. Install the CLI

    .. code-block::

      brew update && brew install azure-cli

  .. group-tab:: Windows

      #. Download the installer from `the docs page <https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest?WT.mc_id=pycon_tutorial-github-taallard>`_
      #. When downloaded, open the driver to follow the instructions.

  .. group-tab:: Linux

    The instructions vary depending on your distribution. Please follow the
    instructions in the `official docs <https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest?WT.mc_id=pycon_tutorial-github-taallard>`_

- Para poder executar e testar suas funções localmente, precisamos instalar as ferramentas básicas de funções do Azure:

.. tabs::

  .. group-tab:: Mac OSX

    #. Install homebrew
    #. Install the CLI

    .. code-block::

      brew tap azure/functions
      brew install azure-functions-core-tools@3
      # if upgrading on a machine that has 2.x installed
      brew link --overwrite azure-functions-core-tools@3

  .. group-tab:: Windows

      #. Install `Node.js <https://docs.npmjs.com/getting-started/installing-node#osx-or-windows>`_
      #. Install the core tools package

      .. code-block::

        npm install -g azure-functions-core-tools@3

  .. group-tab:: Linux

    For Debian/Ubuntu distributions:

    1. Instale a chave GPG do repositório de pacotes da Microsoft para validar a integridade do pacote:

      .. code-block::

        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg  sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

    2. Configure a lista de fontes de desenvolvimento do .NET antes de fazer uma atualização de APT.

      .. code-block::

        # <a name="ubuntu"></a>Ubuntu
        sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu- $(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'

        # <a name="debian"></a>Debian

        sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/debian/ $(lsb_release -rs | cut -d'.' -f 1)/prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'

    3. Inicie a atualização de fonte de APT e instale as ferramentas

      .. code-block::

        sudo apt-get update  sudo apt-get install azure-functions-core-tools

    Para obter instruções mais detalhadas, acesse `corresponding docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=linux%2Ccsharp%2Cbash?WT.mc_id=pycon_tutorial-github-taallard>`_.

<a name="other-accounts"></a>Outras contas
----------------

API StackOverFlow
*******************

Usaremos a API StackOverFlow para coletar dados. Para isso, você precisará se registrar para obter uma chave de aplicativo.

#<a name="-head-over-to-httpsapistackexchangecom_-and-click-on-register-for-an-app-key-note-that-you-will-need-to-log-into-stackoverflow-to-get-a-ner-key"></a>. Vá até `<https://api.stackexchange.com/>`_ e clique em Registrar-se para obter uma chave de aplicativo. Observe que você precisará entrar no StackOverFlow para obter uma chave ner.
#<a name="-in-the-following-screen-you-will-need-to-provide-the-details-of-the-app-they-do-not-have-to-be-extensive-but-you-can-always-go-back-and-change-them-later-once-filled-in-click-on-the-register-app-button"></a>. Na tela seguinte, forneça os detalhes do aplicativo. Eles não precisam ser abrangentes, mas você pode voltar a qualquer momento e alterá-los mais tarde. Depois de preencher os detalhes, clique no botão Registrar aplicativo.

    .. image:: _static/images/snaps/stack.png
            :align: center
            :alt: StackOverFlow
#<a name="-the-next-screen-will-display-your-apps-details-make-sure-to-keep-the-key-and-the-client-secret-safe-at-all-times"></a>. A tela seguinte exibirá os detalhes do seu aplicativo. Mantenha a chave e o segredo do cliente seguros o tempo todo.


.. GitHub .. *******************

.. Você também precisará de uma conta do GitHub para manter seu código em controle de versão e criar uma ação do GitHub para implantar sua função.

.. Se ainda não tiver uma conta, vá até `<https://github.com>`_ e registre-se para obter uma nova conta.
