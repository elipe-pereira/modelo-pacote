#####Modelo de pacote
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

