.. _functions101:


<a name="light-your-first-azure-function"></a>|light| Sua primeira função do Azure
=====================================

Vamos começar criando sua primeira função do Azure.
Utilizaremos o VS Code para criar uma função que funcione todos os dias no mesmo horário.


<a name="creating-your-local-project"></a>Crie seu projeto local
----------------------------

#<a name="-create-a-new-folder-on-your-local-computer-this-is-where-your-function-project-will-live"></a>. Crie uma pasta no computador local. Seu projeto de função ficará armazenado nela.

    For example, if using the command line (bash):

    .. code-block:: bash

        mkdir python-functions

        cd python-functions

#<a name="-start-vs-code-in-the-project-folder-workspace"></a>. Inicie o VS Code na pasta do projeto (workspace)

    You can use the command line like so:

    .. code-block:: bash

        code .

#<a name="-click-on-the-azure-icon-on-your-activity-bar-3-in-the-image"></a>. Clique no ícone do Azure na barra de atividade (3 na imagem)
#<a name="-then-in-the-azure-functions-area-select-the-create-new-project-icon-4-in-the-image"></a>. Em seguida, na área de funções do Azure, selecione o ícone Criar projeto (4 na imagem)

    .. image:: _static/images/snaps/vs_code_functions1.png
        :height: 600px
        :align: center
        :alt: VS code sidebar icons

#<a name="-provide-the-following-information"></a>. Forneça as seguintes informações:

    - **Selecione a pasta que conterá o projeto**: escolha a pasta atual ou selecione uma diferente
    - **Selecione uma linguagem**: Python
    - **Selecione um alias Python para criar um ambiente virtual**: selecione o intérprete Python preferencial (precisa ser compatível)
    - **Selecione um modelo**: gatilho de temporizador
    - **Forneça um nome de função**: digite um nome para seu projeto (escolhi ``timer-function``)
    - **Insira uma expressão cron**: precisamos especificar quando a função será executada; fazemos isso por meio de expressões cron. Uma expressão cron é uma cadeia de caracteres com seis expressões separadas que representam determinado cronograma por meio de padrões. Para este exemplo, quero que ela seja executada todos os dias às 9:00, então estou usando: ``0 9 * * * *``

    .. image:: _static/images/snaps/chron.png :align: center :alt: cron expresion example

.. note:: O fuso horário padrão no Azure Functions é UTC. Dependendo do fuso horário e da finalidade, talvez seja necessário ajustar isso.

A extensão criará um `Python virtual environment <https://docs.python.org/3/tutorial/venv.html>`_, bem como vários arquivos para a função:

.. code-block:: bash

    .
    ├── timer-function
    │   ├── __init__.py
    │   ├── function.json
    │   ├── readme.md
    │   └── sample.dat
    ├── .funcignore
    ├── .gitignore
    ├── host.json
    ├── local.settings.json
    ├── proxies.json
    └── requirements.txt

<a name="the-basics-of-your-new-function"></a>Conceitos básicos da sua nova função
----------------------------------

O arquivo ``function.json`` fornece a configuração principal da sua função:

.. code-block:: json :name: function.json :caption: function.json

    {
        "scriptFile": "__init__.py",
        "bindings": [
            {
            "name": "mytimer",
            "type": "timerTrigger",
            "direction": "in",
            "schedule": "0 9 * * * *"
            }
        ]
    }

Você observará que há um elemento ``bindings``. Ele é marcado como ``"direction": "in"``, que corresponderá ao sinal de entrada para disparar a função.
Nesse caso, estamos usando uma expressão cron para disparar a função todos os dias às 9:00.

Você também observará que há um script ``__init__.py`` (que também é o arquivo de script descrito em ``function.json`` acima).

.. code-block:: python :name: __init__.py :caption: __init__.py


    import datetime
    import logging

    import azure.functions as func


    def main(mytimer: func.TimerRequest) -> None:
        utc_timestamp = (
            datetime.datetime.utcnow().replace(tzinfo=datetime.timezone.utc).isoformat()
        )

        if mytimer.past_due:
            logging.info("The timer is past due!")

        logging.info("Python timer trigger function ran at %s", utc_timestamp)


<a name="running-your-function-locally"></a>Executar sua função localmente
-------------------------------

Agora que inspecionamos a função, estamos prontos para executá-la localmente. Você pode fazer isso pressionando :kbd:`F5`.
Isso iniciará a extensão de depuração.
Como estamos usando o gatilho de temporizador, precisamos configurar uma conta de armazenamento do Azure. Ela servirá principalmente para manter os logs e outras saídas. Portanto, você poderá receber o aviso a seguir na primeira vez que tentar executar a função localmente.

.. image:: _static/images/snaps/storage.png :align: center :alt: Depurador do VS Code – adicionar armazenamento

Nas janelas seguintes, selecione estas opções:

- Criar uma conta de armazenamento: certifique-se de dar a ela um nome significativo (apenas letras e números são aceitos)
- **Grupo de recursos**: queremos que todos os nossos serviços fiquem juntos, portanto, opte por criar um grupo de recursos e dê a ele um nome
- **Região**: corresponde ao data center onde seus recursos ficarão localizados (por exemplo, EUA Central)

.. note:: Você precisará estar conectado ao Azure para poder criar sua conta de armazenamento. Se precisar de ajuda com essa tarefa, confira :ref:`login_azure`.

Depois que sua conta de armazenamento for criada (se necessário), você deverá ver a saída da função do Azure em seu terminal.

.. image:: _static/images/snaps/functions_debug.png :align: center :alt: Executar funções localmente

Se eu alterar a expressão cron para ser executada a cada hora, dez minutos após o horário ``10 */1 * * * *``, para fins de demonstração, deverei ver o prazo da função na saída do console:

.. code-block:: bash

    [15/04/2020 19:28:58] The next 5 occurrences of the 'timer-function' schedule (Cron: '10 * * * * *') will be:
    [15/04/2020 19:28:58] 04/15/2020 20:29:10+01:00 (04/15/2020 19:29:10Z)
    [15/04/2020 19:28:58] 04/15/2020 20:30:10+01:00 (04/15/2020 19:30:10Z)
    [15/04/2020 19:28:58] 04/15/2020 20:31:10+01:00 (04/15/2020 19:31:10Z)
    [15/04/2020 19:28:58] 04/15/2020 20:32:10+01:00 (04/15/2020 19:32:10Z)
    [15/04/2020 19:28:58] 04/15/2020 20:33:10+01:00 (04/15/2020 19:33:10Z)
    [15/04/2020 19:28:58] Host started (1961ms)
    [15/04/2020 19:28:58] Job host started
    Hosting environment: Production
    Content root path: /myuser/demos/functions-python
    Now listening on: http://0.0.0.0:7071
    Application started. Press Ctrl+C to shut down.



Mais abaixo na saída, você deverá ver quando é o próximo prazo da função:

Para interromper a função, você pode pressionar kbd:`CTRL + C`.



.. _login_azure:

<a name="log-into-azure-from-vs-code"></a>Entrar no Azure pelo VS Code
-----------------------------

1. Se você ainda não tiver entrado, escolha o ícone do Azure na barra de Atividades. No Azure: Na área de funções, selecione Entrar no Azure.

    .. image:: https://docs.microsoft.com/en-us/azure/includes/media/functions-sign-in-vs-code/functions-sign-into-azure.png :alt: VS code sign in :align: center

2. Quando solicitado no navegador, escolha sua conta do Azure e entre usando as credenciais da sua conta do Azure.
3. Depois de entrar com êxito, você poderá fechar a nova janela do navegador. As assinaturas que pertencem à sua conta do Azure são exibidas na barra lateral. Você também deve poder visualizar o email com o qual você entrou na barra de status inferior no VSCode.


<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------

- `Time trigger for Azure functions official docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer?tabs=csharp?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure functions cron cheatsheet <https://arminreiter.com/2015/02/azure-functions-time-trigger-cron-cheat-sheet/>`_
- `Cron generator <https://crontab.guru/#0_9_*_*_*>`_
- `Cron tab cheatsheet <https://www.codementor.io/@akul08/the-ultimate-crontab-cheatsheet-5op0f7o4r>`_
- Um blog útil sobre como lidar com `Time Zones <https://dev.to/azure/getting-rid-of-time-zone-issues-within-azure-functions-4066>`_ nas funções do Azure
- Funções do Azure `project structure docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp#generated-project-files?WT.mc_id=pycon_tutorial-github-taallard>`_
- Expressão cron humana `descriptor <https://cronexpressiondescriptor.azurewebsites.net/>`_ muito útil se você estiver apenas se familiarizando as expressões cron
- `Python type hints cheatsheet <https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html>`_ 
