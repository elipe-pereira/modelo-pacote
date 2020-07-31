# Modelo de pacote
### Objetivos
  * Servir como base para a criação de novos pacotes .deb linux
  * Garantir o máximo de rapidez e padronização na instalação dos clientes.

#### Estrutura básica
RAIZ

  |_ DEBIAN
           |_control
           |_prerm
           |_postrm
           |_preinst
           |_postinst
  |_usr
       |_share
              |_modelo_pacote
                             |_arquivo01
                             |_arqruivo02
  |_etc
       |_modelo_pacote
                      |_arquivo01.conf

Para a criação de um pacote .deb para as distribuições ubuntu/debian
é obrigatório exisitir a pasta de DEBIAN (em maísculo) como os respectivos arquivos
exibidos na estrutura básica. 


### control
O arquivo control precisa conter as seguintes linhas: 

Section: misc

Package: modelo_pacote

Priority: optional

Version: 0.1

Architecture: all

Maintainer: Eli Florêncio Pereira

Depends: pacote, pacote2

Description: Descrição que aparece quando vc dá um apt-cache search 

##### Section

Define uma seção para o pacote, como os nosso pacotes não fazem parte do repositório
oficial, o ideal é deixar como misc

##### Package

É o nome do pacote .deb que será gerado. Quando vc for instalar, ex: apt-get install modelo_pacote
é por causa desse parâmetro que define o nome. 

#####  Priority

Não é obrigatório, sempre deixe como optional

##### Version: 0.1

Ao construir o pacote, a versão será incluída no nome do pacote e será inserida na base de dados do repositório. 
Ao commitar uma nova versão esse valor deve mudar para que o pacote anterior seja substituído. 

##### Architecture

As três possível são amd64, i386 e all para noarch. Se você compilou o pacote, você deve colocar em que arquitetura
ele foi compilado (amd64 ou i386), caso contrário você deve somente colocar all. 

##### Maintainer

É o nome do mantenedor do pacote, quando foi usado o comando apt-cache show modelo_pacote, o nome do mantainer
aparecerá. Geralmente é colocado também um e-mail para contato ao lado.

##### Depends

Aqui são inseridos todos os pacotes ao qual seu programa depende. Se não estiver instalado, o apt instalará junto antes de executar a instalação do pacote. 

##### Description

É uma descrição do pacote. É o que vai aparecer quando for usado o comando apt-cache search modelo_pacote.

### prerm

Nesse arquivo são colocados os comandos pre remoção do pacote. Em geral, não é recomedado colocar nada nele ao não ser que seja realmente necessário. Ex:

#!/bin/bash

service apache2 stop

---fim do arquivo---

### postrm

Nesse arquivo são colocados os comandos pós remoção do pacote. Também não é recomendado a inserção de comandos aqui, a não ser que seja realmente necessário. 

### preinst

Nesse arquivo são colocados comandos pré instalação. Por exemplo, no caso onde o pacote cujo seu programa depende não tem biblioteca no apt mas tem 
no repositório pip(python) ou cpamn(perl).
ex:
#!/bin/bash
pip install setuptools
cpanm -nf --skip-installed Text::Glob
---fim do arquivo--

Obs: é sempre bom colocar um || echo "ok" no final do comando. ex: pip install setuptools || echo "ok"

para que caso você tenha digitado algo errado, na hora de instalar o pacote não fique acusando erro na instalação do pacote. 

### postinst

Nesse arquivo vão os comandos pós instalação. Não é obrigado colocar nada nele, mas caso precise reiniciar um serviço após
 a instalação por exemplo, é nesse arquivo que você colocará o comando. 
 
 #!/bin/bash
 service apache2 restart

-- fim do arquivo--

## Sobre as pastas usr e etc

O restante das pastas seguem a estrutura do sistema operacional linux. Se no repositório os arquivos estivem dentro usr/share/arquivos, quando
o apt-get descompactar o arquivo .deb, ele terá a mesma estrutura no sistema operacional Linux onde foi instado. ex: /usr/share/arquivos. 

No caso do modelo_pacote, a estrutura é usr/share/modelo_pacote e etc/modelo_pacote.

Quando eu instalar no sistema operacional, as pastas serão coladas respectivamente em /usr/share/modelo_pacote e /etc/modelo_pacote. 

