# Sobre o projeto

Ticketz é um comunicador com recursos de CRM e helpdesk que utiliza
Whatsapp como meio de comunicação com os clientes.

## Autoria original

Este projeto foi iniciado em [um projeto Open
Source](https://github.com/canove/whaticket-community), publicado pelo
desenvolvedor [Cassio Santos](https://github.com/canove) sob a licença permissiva
MIT. Depois recebeu diversas melhorias por autores não identificados e foi
comercializado diretamente entre desenvolvedores e usuários com fornecimento
de código fonte, e de acordo com informações [deste vídeo acabou em algum momento
sendo vazado e publicado abertamente](https://www.youtube.com/watch?v=SX_cGD5RLkQ)

Após algumas pesquisas foi ainda identificado que a primeira versão SaaS do
Whaticket foi criada pelo desenvolvedor [Wender
Teixeira](https://github.com/w3nder), inclusive uma versão do [https://github.com/unkbot/whaticket-free](Whaticket
Single) que faz uso da biblioteca Baileys para acesso ao Whatsapp.

É praticamente impossível identificar e creditar os autores das melhorias, [o
código publicado pelo canal Vem Fazer](https://github.com/vemfazer/whaticket-versao-03-12-canal-vem-fazer)
não menciona licença alguma portanto estou presumindo que todos os autores
estão tranquilos em manter estas alterações sob a mesma licença do projeto
original (MIT)

## Relicenciamento

Como estou fazendo estas alterações e disponibilizando sem custo algum, desejo que
elas estejam disponíveis a todos, por isso estou optando por relicenciar sob a
AGPL, que exige que todo usuário que tenha acesso ao sistema possa obter o
código fonte.

Por isso, se você utilizar diretamente esta versão, é
**muito importante manter o link na tela "Ajuda", que dá acesso ao repositório**.

Caso você faça alterações no código você deve alterar o link para um
repositório ou outra forma de obter o código das suas alterações.

## Objetivo

Este projeto tem por objetivo melhorar e manter abertas as atualizações sobre o Whaticket
SaaS publicado. Principalmente direcionadas à qualidade da aplicação e à
facilidade de instalação e utilização.

As melhorias desenvolvidas por mim serão colocadas aqui, dependendo posso transpor,
sempre creditando, códigos e melhorias publicados em outros projetos também derivados
do Whaticket Community ou do Whaticket SaaS.

## Melhorias

Por melhor esforço, procurarei sempre listar aqui as melhorias incorporadas, creditando
autorias quando necessário, porém o melhor local para observar o que foi feito é o histórico
do repositório.

* [83f6713](https://github.com/allgood/ticketz/commit/83f67132c234f528c13540b3de529ccb54cc3e6a) Aceita documento anexado com legenda)
* [e8f4d32](https://github.com/allgood/ticketz/commit/e8f4d325f46133a2ea828dfe8ca7470f44243bf5) Aceita mensagens editadas -- cherry pick de @Vinicius-Marques6 canove/whaticket-community#605
* [60455d9](https://github.com/allgood/ticketz/commit/60455d9416975a0d1806968815d28f5195d15e64) Mantém aberto e utiliza apenas um websocket com o backend
* [30526b6](https://github.com/allgood/ticketz/commit/30526b6cd6d92e3204e97ff194ef57b7def69979) Um ticket novo ao invés de reabrir ticket fechado
* [2b58d6c](https://github.com/allgood/ticketz/commit/2b58d6c1c424bbcb060f9cc7196bfde4b42926ff) Execução através do docker compose - **Múltiplos commits até esse ponto**
* [851bca1](https://github.com/allgood/ticketz/commit/851bca1b4d048a6f31ad90ad1db67c37dde3bcf3) Suporte recaptcha na inscrição de empresas

## Contribuindo de Volta

Sempre que possível pretendo fazer backport de alguns ajustes feitos aqui
aos projetos originais


Rodando o projeto:
------------------

O projeto atualmente suporta execução utilizando containers Docker, para a
instalação é necessário ter o Docker Community Edition e o cliente Git
instalados. O ideal é buscar a melhor forma de instalar estes recursos no
sistema operacional de sua preferência. [O guia oficial de instalação do
Docker pode ser encontrado aqui](https://docs.docker.com/engine/install/).


Em ambos os casos é necessário clonar o repositório, necessário então abrir
um terminal de comandos:

```bash
git clone https://github.com/allgood/ticketz.git
cd ticketz
```

## Rodando localmente

Por padrão a configuração está ajustada para executar o sistema apenas no
próprio computador. Para executar em uma rede local é necessário editar os
arquivos `.env-backend-local` e `.env-frontend-local` e alterar os endereços
de backend e frontend de `localhost` para o ip desejado, por exemplo
`192.168.0.10`

Para executar o sistema basta executar o comando abaixo:

```bash
docker compose -f docker-compose-local.yaml up -d
```

Na primeira execução o sistema vai inicializar os bancos de dados e tabelas,
e após alguns minutos o Ticketz estará acessível pela porta 3000

O usuário padrão é admin@admin.com e a senha padrão é 123456

A aplicação irá se reiniciar automaticamente a cada reboot do servidor.

A execução pode ser interrompida com o comando:

```bash
docker compose -f docker-compose-local.yaml down
```


## Rodando e servindo na internet

Tendo um servidor acessível pela internet, é necessário ajustar dois nomes
de DNS a sua escolha, um para o backend e outro para o frontend, e também um
endereço de email para cadastro dos certificados, por exemplo:

* **backend:** api.ticketz.exemplo.com.br
* **frontend:** ticketz.exemplo.com.br
* **email:** ticketz@exemplo.com.br

É necessário editar os arquivos `.env-backend-acme` e `.env-frontend-acme`
definindo neles estes valores.

Se desejar utilizar reCAPTCHA na inscrição de empresas também é necessário
inserir as chaves secretas e de site nos arquivos de backend e frontend,
respectivamente.

Este guia presume que o terminal está aberto e logado com um usuário comum
que tem permissão para utilizar o comando `sudo` para executar comandos como
root.

Estando então na pasta raiz do projeto, executa-se o seguinte comando para
iniciar o serviço:

```bash
sudo docker compose -f docker-compose-acme.yaml up -d
```

Na primeira execução o Docker irá fazer a compilação do código e criação dos
conteiners, e após isso o ticketz vai inicializar os bancos de dados e
tabelas. Esta operação pode levar bastante tempo, depois disso o Ticketz
estará acessível pelo endereço fornecido para oo frontend.

O usuário padrão é admin@admin.com e a senha padrão é 123456

A aplicação irá se reiniciar automaticamente a cada reboot do servidor.

Para encerrar o serviço utiliza-se o seguinte comando:

```bash
sudo docker compose -f docker-compose-acme.yaml down
```

Aviso Importante
----------------

Este projeto não está afiliado à Meta, WhatsApp ou qualquer outra empresa.
A utilização do código fornecido é de responsabilidade exclusiva dos usuários
e não implica em qualquer responsabilidade para o autor ou colaboradores do projeto.


Facilitou sua vida?
-------------------

Se este projeto ajudou você em uma tarefa complexa, considere fazer uma doação ao autor pelo PIX abaixo.

![image](https://github.com/ticketz-oss/ticketz/assets/6070736/8e85b263-73ca-4fb4-9bdc-03fff356b6ff)

Chave Pix: 0699c69d-0951-4686-a5b7-c6cd21aa7e15
