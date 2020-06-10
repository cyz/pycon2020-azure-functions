<a name="pipe-adding-blob-storage-bindings"></a>|pipe| Adicionar associações do Armazenamento de Blobs
====================================

Agora você deve ter uma função operacional que coleta dados da API StackExchange.

Nesta seção, iremos:

- Concluir a função para armazenar os dados no Armazenamento de Blobs do Azure
- Criar uma segunda função que identifica a adição de um arquivo no Armazenamento de Blobs do Azure e dispara uma segunda função
- Criar um banco de dados para armazenar nossos dados limpos e modificar a função para armazenar o banco de dados

.. tip:: O repositório que contém todos os scripts e soluções para este tutorial pode ser encontrado em `<https://github.com/trallard/pycon2020-azure-functions>`_.

    👉🏼 The code for this section is located in `<https://github.com/trallard/pycon2020-azure-functions/tree/master/solutions/02-timer-function-Blob-binding>`_ 


<a name="light-triggers-and-bindings"></a>|light| Gatilhos e associações
--------------------------------

- **Gatilhos**: fazem com que uma função seja executada. Eles podem ser uma solicitação HTTP, uma mensagem de fila ou uma grade de eventos. Cada função **precisa** ter um gatilho.

- **Associação**: é uma conexão entre uma função e outro recurso ou função. Elas podem ser *associações de entrada, associações de saída* ou ambas. Elas são opcionais, e uma função pode ter uma ou mais associações.

1. Criar o Armazenamento de Blobs do Azure
******************************************

Já criamos uma Conta de Armazenamento na seção :ref:`deployfn`. A próxima etapa é criar um contêiner de Armazenamento de Blobs para que possamos começar a salvar os dados coletados por meio de sua função.

#<a name="-head-over-to-azureportal-and-click-on-storage-accounts-on-the-left-sidebar-and-then-on-your-function-storage-account"></a>. Vá para o |azureportal| e clique em **Contas de armazenamento** na barra lateral esquerda e, em seguida, em sua conta de armazenamento de função.

    .. image:: _static/images/snaps/storagedashboard.png
        :align: center
        :alt: Storager dashboard

#<a name="-click-on-either-of-the-containers-section-see-image"></a>. Clique em uma das seções **Contêineres** (confira a imagem).

    .. image:: _static/images/snaps/containers.png
        :align: center
        :alt: Containers screenshot

#<a name="-click-on--container-at-the-top-of-the-bar-and-provide-a-name-for-your-blob-container"></a>. Clique em **+ Contêiner** na parte superior da barra e forneça um nome para o contêiner de Blobs.

#<a name="-without-leaving-your-dashboard-click-on-access-keys-on-the-sidebar-menu-and-copy-the-connection-string"></a>. Sem sair do painel, clique em **Chaves de acesso** no menu da barra lateral e copie a cadeia de conexão.

    .. image:: _static/images/snaps/access.png
            :align: center
            :alt: Storage dashboard access

.. _attachblob:

2. Anexar associação de Blobs
******************************************

Agora que você criou o contêiner de Blobs, precisará adicionar a associação à sua função.

1. De volta ao VS Code, clique na extensão do **Azure** na barra lateral e clique com o botão direito do mouse no nome da função > **Adicionar associação**.
2. Como queremos armazenar as saídas no contêiner, precisamos selecionar a direção **OUT** seguida por **Armazenamento de Blobs do Azure**.
3. Atribua um nome para a associação de um caminho para o blob:

    .. code-block::

        functionblob/{DateTime}.csv

    Observe que estou usando o nome do contêiner que criei antes e a expressão de associação ``DateTime`` que é resolvida para ``DateTime.UtcNow``. O caminho de blob a seguir em um arquivo ``function.json`` cria um blob com um nome como ``2020-04-16T17-59-55Z.txt``.

4. Selecione **AzureWebJobsStorage** para as configurações locais.

Depois de concluído, seu arquivo ``function.json`` deve ter a seguinte aparência:

    .. literalinclude:: ../solutions/02-timer-function-Blob-binding/timer-function/function.json
        :language: json
        :caption: function.json


5. Adicione a **Chave de acesso de armazenamento** que você copiou antes ao seu ``local.settings.json``. Se você adicionou sua conta de armazenamento por meio das extensões de funções do Azure, isso já deve estar preenchido.

    .. code-block:: :caption: local.settings.json :emphasize-lines: 4

        {
            "IsEncrypted": false,
            "Values": {
                "AzureWebJobsStorage": <Your key>,
                "FUNCTIONS_WORKER_RUNTIME": "python",
                "AzureWebJobs.timer-function.Disabled": "false"
            }
        }

.. _blobfunction: 

3. Atualizar sua função
*****************************

Agora, precisamos atualizar a função para ela:

- Salvar os itens de API coletados em um arquivo CSV
- Armazenar o arquivo no contêiner de Blobs

Atualizar o arquivo `main_function.py`:

    .. literalinclude:: ../solutions/02-timer-function-Blob-binding/timer-function/main_function.py
        :language: python
        :caption: main_function.py
        :emphasize-lines: 7, 33-53, 61-63, 87-93

Observe estas linhas no código acima:

.. code-block:: python


        def main(
            mytimer: func.TimerRequest,
            outputBlob: func.Out[bytes],
            context: func.Context
        ) -> None:

O ``outputBlob: func.Out[bytes]`` especifica a associação que acabamos de criar, e ``context: func.Context`` permite que a função obtenha o contexto do arquivo `host.json`.

E também o script para acessar a API StackExchange:

    .. literalinclude:: ../solutions/02-timer-function-Blob-binding/timer-function/utils/stack.py
        :language: python
        :caption: utils/stack.py

Se desejar, você poderá seguir as etapas na seção :ref:`localdebug` para executar e depurar sua função localmente.

Caso contrário, você pode implantar e executar sua função como fizemos na seção :ref:`deployandrun` (exceto para a seção de configuração de variáveis, já que os detalhes de armazenamento já devem estar lá).


.. tip:: Ao implantar sua função, você pode clicar no link da janela pop-up **janela de saída** para acompanhar o status/andamento da implantação.

    .. image:: _static/images/snaps/explore.png
        :align: center
        :alt: Explore deploy

Depois de executar a função, você pode ir para **Contas de armazenamento > <your account> > Contêineres** e clicar no contêiner de blobs de função.

Se tudo funcionar sem problemas, você poderá ver o arquivo criado.

.. image:: _static/images/snaps/blob_file.png :align: center :alt: Arquivo de Blob



<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------

- `ARM template for Blob Storage container <https://github.com/trallard/pycon2020-azure-functions/tree/master/storage-blob-container>`_
- `Azure functions triggers and bindings <https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure functions supported bindings <https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings#supported-bindings?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure Storage documentation <http://azure.microsoft.com/documentation/articles/storage-create-storage-account?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Binding expressions docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-expressions-patterns?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure function reference output <https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python#outputs?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Python type hints cheatsheet <https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html>`_
