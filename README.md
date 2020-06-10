# <a name="snake-easy-data-processing-with-azure-functions-and-python"></a>:snake: Processamento de dados fácil com Azure Functions e Python

[![Documentos](https://img.shields.io/badge/License-MIT-gray.svg?colorA=2D2A56&colorB=7A76C2&style=flat.svg)]((https://opensource.org/licenses/MIT))
![de licença](https://github.com/trallard/pycon2020-azure-functions/workflows/docs/badge.svg)

Este repositório contém o tutorial para o workshop patrocinado do Microsoft Azure. Ele também inclui todas as soluções para as diferentes seções.

<div align="center">
<img src="./docs/_static/icons/MSFT_Logo_Color.png" width="400px">
</div>

:sparkles: Você pode acessar o tutorial (individualizado) em <https://aka.ms/pycon2020-azurefunctions>.

:sparkles: As soluções estão localizadas neste repositório no diretório [Soluções](./solutions).

---

![NOVO](https://img.shields.io/badge/-NEW-gray.svg?colorB=18a4e0)  :video_camera:  Vídeo de tutorial! Vá para o canal do YouTube da PyCon US: <https://www.youtube.com/watch?v=PV7iy6FPjAY>

![NOVO](https://img.shields.io/badge/-NEW-gray.svg?colorB=18a4e0)  :sparkles: Os slides complementares estão no SpeakerDeck <https://speakerdeck.com/trallard/easy-data-processing-on-azure-with-serverless-functions>

---

## <a name="table-of-contents"></a>Sumário

- [:snake: Processamento de dados fácil com funções do Azure e Python](#snake-easy-data-processing-with-azure-functions-and-python)
  - [Sumário](#table-of-contents)
  - [:pencil: Descrição](#pencil-description)
  - [:bookmark: Estrutura](#bookmark-outline)
  - [:computer: Pré-requisitos](#computer-pre-requisites)
  - [:eyes: Soluções](#eyes-solutions)
  - [Licença](#license)

## <a name="pencil-description"></a>:pencil: Description

A computação sem servidor (também conhecida como função como serviço, FaaS) é um padrão de design em que os aplicativos são hospedados por um serviço de terceiros (ou seja, o Azure), eliminando a necessidade de gerenciamento de hardware e software do servidor pelo desenvolvedor.

A computação sem servidor pode ser uma excelente alternativa para Pythonistas interessados no processamento de dados, pois permite que eles se concentrem no código, e não na infraestrutura de nuvem. Este workshop apresentará aos participantes o Azure Functions para cenários de processamento de dados (incluindo aquisição de dados, limpeza e transformação e armazenamento para uso posterior).

Após este tutorial, os participantes terão experiência prática com as funções do Azure para cenários de processamento de dados. Além disso, eles deixarão o workshop com uma função básica para processamento de dados que pode ser modificada/ampliada para atender às suas necessidades/requisitos.

## <a name="bookmark-outline"></a>:bookmark: Estrutura

1. Introdução à computação sem servidor e às funções do Azure
2. Como criar sua primeira função do Azure:
   - Criar uma função agendada simples usando a extensão do VS Code
   - Familiarizar-se com a estrutura e os projetos de funções
   - Como executar e depurar localmente
3. Implantação de funções
   - Implantar sua função no Azure
   - Familiarizar-se com o portal do Azure
4. Caso de uso de processamento de dados
   - Como atualizar sua função para coletar dados
   - Limpeza de dados, agregação e armazenamento

## <a name="computer-pre-requisites"></a>:computer: Pré-requisitos

Este workshop destina-se a pessoas interessadas em processamento de dados, engenharia de dados ou ciência de dados. O objetivo é fornecer uma introdução prática à computação sem servidor para cenários de processamento de dados.

Supomos que você:

- Tenha conhecimento intermediário de Python:
  - Tenha uma boa compreensão de como escrever e chamar funções
  - Tenha um bom conhecimento de como funcionam os módulos e scripts do Python

- Tenha alguma experiência com estruturação de dados e/ou processamento de dados (não é necessária uma ampla experiência, mas ter usado, por exemplo, bibliotecas como Pandas e solicitações de estruturação de dados e acesso a API)

- Sinta-se confortável ao usar a linha de comando/terminal (não é necessário ser um especialista, mas se sentir confortável o suficiente para navegar pelos sistemas de arquivos e executar tarefas necessárias do Git)

## <a name="eyes-solutions"></a>:eyes: Soluções

As soluções podem ser encontradas no [diretório de soluções](./solutions) neste repositório.

- Função de temporizador: [Somente aquisição de dados de API](./solutions/01-timer-function-data-acquisition/)
- Função de temporizador: [API + Associação de Blobs](./solutions/02-timer-function-Blob-binding/)
- Função de temporizador + Processamento de dados/envio de emails: [pipeline completo](./solutions/03-full-pipeline/)

Modelos de ARM incluídos:

- [Conta de armazenamento e Armazenamento de Blobs](./solutions/../storage-blob-container/azuredeploy.json)

## <a name="key-license"></a>:key: Licença

O conteúdo deste repositório é licenciado sob a licença [https://opensource.org/licenses/MIT](MIT) OSI.

Os ícones usados no tutorial são de [Smashicons](https://www.flaticon.com/authors/smashicons) da [Flaticon](https://www.flaticon.com/).
