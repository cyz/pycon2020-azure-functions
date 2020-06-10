<a name="api-data-acquisition-with-functions"></a>|api| Aquisição de dados com funções
=========================================

Já temos uma função operacional e implantada, mas até agora ela não está fazendo nada de interessante.

Vamos começar a trabalhar na parte de processamento de dados da função.

.. tip:: O repositório que contém todos os scripts e soluções para este tutorial pode ser encontrado em `<https://github.com/trallard/pycon2020-azure-functions>`_.

    👉🏼 The code for this section is located in `<https://github.com/trallard/pycon2020-azure-functions/tree/master/solutions/01-timer-function-data-acquisition>`_ 


<a name="the-details"></a>Os detalhes
-------------
Para demonstrar os recursos das funções do Azure para cenários de processamento de dados, criaremos o seguinte pipeline:

#<a name="-collect-data-from-the-stackexchange-api-httpsapistackexchangecom_-using-the-timer-trigger-we-will-focus-on-extracting-questions-from-stackoverflow-within-a-time-range-and-with-specific-tags"></a>. Coletar dados da `StackExchange API <https://api.stackexchange.com/>`_ usando o gatilho de temporizador. Focaremos em extrair perguntas do StackOverflow dentro de um intervalo de tempo e com marcas específicas.
#<a name="-store-the-raw-data-in-our-azure-storage-account"></a>. Armazenar os dados brutos em nossa conta de armazenamento do Azure.
#<a name="-trigger-the-processing-function-that-cleans-the-data-and-leaves-it-in-a-usable-format"></a>. Disparar a função de processamento que limpa os dados e os deixa em um formato utilizável.

Vamos começar!

<a name="connecting-to-the-stackexchange-api"></a>Conectar-se à API StackExchange
-------------------------------------

1. Criar os arquivos e diretórios necessários
*********************************** 

Na seção :ref:`functions101`, criamos uma função de temporizador básica e exploramos os arquivos gerados.

Para manter a organização, criaremos também uma pasta ``utils`` e arquivos ``__init__.py`` e ``stack.py`` nela. Na linha de comando (bash):

.. code-block:: bash

    mkdir -p <your-function-dir>/utils
    touch <your-function-dir>/utils/__init__.py 
    touch <your-function-dir>/utils/stack.py 


2. Adicionar métodos 
*****************************

Agora que temos os arquivos necessários, precisamos atualizar ``utils/stack.py`` para lidar com as solicitações feitas para a API StackExchange:

.. literalinclude:: ../solutions/01-timer-function-data-acquisition/timer-function/utils/stack.py :language: python :caption: utils/stack.py

Observe como usamos o tempo de disparo para definir ``todate`` e ``fromdate`` na consulta de StackExchange. 

Portanto, também precisamos modificar o script principal de nossa função:

.. literalinclude:: ../solutions/01-timer-function-data-acquisition/timer-function/main_function.py :language: python :caption: __init__.py

3. Organizar e concluir
*****************************

1. Para facilitar a identificação dos arquivos, renomearemos o script de função para ``main_function.py``:

    .. image:: _static/images/snaps/main_function.png :align: center :alt: Nome da função

.. warning:: Você também precisa alterar o nome do ``scriptFile`` no arquivo ``function.json``. Caso contrário, sua função não será capaz de localizar o arquivo.

2. Como estamos usando *solicitações* e *python-dotenv*, precisamos atualizar o arquivo ``requirements.txt``:

.. literalinclude:: ../solutions/01-timer-function-data-acquisition/requirements.txt :language: python :caption: requirements.txt

3. Por fim, precisamos criar um arquivo ``.env`` para armazenar chaves de API e outras variáveis de ambiente para desenvolvimento e depuração locais. 

.. code-block:: :caption: .env

    # Stackexchange

    SE_client_id = <your secret>
    SE_client_secret = <your secret>
    SE_key = <your secret>


.. warning:: **Não** confirme esse arquivo .env para o controle de versão. Aprenderemos posteriormente no tutorial como adicionar variáveis às suas funções do Azure com segurança. 

.. _localdebug:

4. Depurar e executar localmente
*************************************

#<a name="-start-the-debugging-session-in-vs-code-by-pressing-kbdf5-you-should-see-the-function-output-in-the-integrated-terminal"></a>. Inicie a sessão de depuração no VS Code pressionando :kbd:`F5`. Você deve ver a saída da função no terminal integrado. 
#<a name="-click-on-the-azure-extension-on-the-vs-code-sidebar-and-then-expand-the-functions-section"></a>. Clique na extensão do **Azure**  na barra lateral do VS Code e expanda a seção Funções.
#<a name="-right-click-on-your-function-name-timer-function-and-click-on-execute-function-now"></a>. Clique com o botão direito do mouse no nome da função (função temporizador) e clique em **Executar função agora**. 

.. image:: _static/images/snaps/debug_function.png :align: center :alt: Função de depurador

Se tudo tiver sido atualizado corretamente, você deverá ver a saída da função no terminal integrado do VS Code.

.. code-block:: bash

    [15/04/2020 14:03:34] Executing 'Functions.timer-function' (Reason='This function was programmatically called via the host APIs.', Id=d900f28c-10e5-4e40-8de1-a17079674139)
    [15/04/2020 14:03:34]  INFO: Received FunctionInvocationRequest, request ID: 4bab6cbc-a5eb-4ce9-9cb5-4580ca431de3, function ID: c8491e7b-4c49-4546-9a0a-5a07ba7e2020, invocation ID: d900f28c-10e5-4e40-8de1-a17079674139
    [15/04/2020 14:03:34] Function executing at 2020-04-15T14:03:34.755770+00:00
    [15/04/2020 14:03:34] Dotenv located, loading vars from local instance
    [15/04/2020 14:03:35] 🐍 Collected 30 new questions for the search term
    [15/04/2020 14:03:35]  INFO: Successfully processed FunctionInvocationRequest, request ID: 4bab6cbc-a5eb-4ce9-9cb5-4580ca431de3, function ID: c8491e7b-4c49-4546-9a0a-5a07ba7e2020, invocation ID: d900f28c-10e5-4e40-8de1-a17079674139
    [15/04/2020 14:03:35] Executed 'Functions.timer-function' (Succeeded, Id=d900f28c-10e5-4e40-8de1-a17079674139)

.. _deployandrun:

5. Implantar sua função atualizada
************************************

Primeiro, certifique-se de interromper o localhost. Você pode fazer isso pressionando as teclas :kbd:`Ctrl + C` ou clicando no botão desconectar da barra de depuração:

.. image:: _static/images/snaps/disconnect.png :align: center :alt: Desconectar

Para implantar sua função atualizada:

1. Clique na extensão do Azure na barra lateral do VS Code e, em seguida, clique em implantar para o aplicativo de funções na seção de funções do Azure.

2. Selecione o nome do aplicativo que você usou antes (já que queremos atualizar a instância existente).

    .. image:: _static/images/snaps/redeploy.png :align: center :alt: Confirmar Implantação

3. Acesse o |azureportal| e siga as mesmas instruções de :ref:`portalinst` para ir até a página principal da sua função:

    .. image:: _static/images/snaps/configuration.png :align: center :alt: Configuração da função

4. Clique em **Configuração** e, na tela seguinte, clique em + **Nova configuração de aplicativo** (1 na imagem) para adicionar as chaves armazenadas em seu arquivo ``.env`` local.
Adicione um por um como um par de valor separado (deve ser semelhante a 2 na imagem).

    .. image:: _static/images/snaps/vars.png :align: center :alt: Configurações de variáveis 

5. Depois de concluído, clique no botão Salvar na barra superior (3 na imagem acima).
6. Execute sua função na nuvem: volte para a página principal da função no |azureportal|. Em seguida, clique no nome da sua função (1 na imagem abaixo) e, em seguida, no botão **Executar** no canto superior direito (2 na imagem).

    .. image:: _static/images/snaps/vars.png :align: center :alt: Executar a função na nuvem

Agora, você pode ir para a seção monitor de sua função e ver os logs e o status da execução que acabou de iniciar.

<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------

- `Stack Exchange API docs <https://api.stackexchange.com/docs/>`_ 
- `Azure functions management <https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings?WT.mc_id=pycon_tutorial-github-taallard>`_ 
