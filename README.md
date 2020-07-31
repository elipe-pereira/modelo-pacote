##### Modelo de pacote
## Objetivos
  * Servir como base para a criação de novos pacotes .deb linux

## Estrutura básica
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

O arquivo control precisa conter as seguintes linhas: 

Section: misc
Package: modelo_pacote
Priority: optional
Version: 0.1
Architecture: all
Maintainer: Eli Florêncio Pereira
Depends: pacote, pacote2
Description: Descrição que aparece quando vc dá um apt-cache search 

## Section

Define uma seção para o pacote, como os nosso pacotes não fazem parte do repositório
oficial, o ideal é deixar como misc

## Package

É o nome do pacote .deb que será gerado. Quando vc for instalar, ex: apt-get install modelo_pacote
é por causa desse parâmetro que define o nome. 

##  Priority

Não é obrigatório, sempre deixe como optional

## Version: 0.1

Ao construir o pacote, a versão será incluída no nome do pacote e será inserida na base de dados do repositório. 
Ao commitar uma nova versão esse valor deve mudar para que o pacote anterior seja substituído. 