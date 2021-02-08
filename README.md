
# DOCKER INSTALACAO
>>>> https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-9-pt
- sudo apt update
- udo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
- curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
- sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
- sudo apt update
- apt-cache policy docker-ce
- sudo apt install docker-ce
- sudo systemctl status docker
- sudo usermod -aG docker username
# DOCKER PORTAINER
- docker volume create portainer_data
- docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

# DOCKER HUB - PUSH

- A PARTIR DO CONTAINER (ATUALIZADO COM OS PACOTES) CRIAR UMA IMAGEM ATRAVES DO COMIT
- docker commit phdshiny phdshiny:v2020.03.13 {cria uma imagem do container phdshiny}
- criar um tag phdshiny:v2020.03.13 phdriskdocker/shiny:v2020.03.13
- docker push phdriskdocker/shiny:v2020.03.13

- ****** IMPORTANTE ******

* PARA MOVER OS ARQUIVOS, CRIE UMA PASTA FORA DO SHINY-SERVER, "/home/rstudio/arquivos"
* ENTRE NO PROMPT USANDO O PORTAINER E FACA UMA COPIA PARA ESTA PASTA 
* -> cp /home/rstudio/shiny-server/ * -R /home/rstudio/arquivos
*
* DEPOIS DE EXECUTAR O IMAGES, ABRE O RSTUDIO E ATRAVES DELE MOVA  OS ARQUIVOS PARA DENTRO DA PASTA SHINY-SERVER


# DOCKER HUB - PULL
- docker pull phdriskdocker/shiny:v2020.03.13
- docker run -d -itd -p 3838:3838 -v /srv/shinyapps:/srv/shiny-server -v /srv/shinylog:/var/log/shiny-server --name phdshiny phdriskdocker/shiny:v2020.03.13

# DOCKER ( SHINY E RSTUDIO) - UTILIZANDO MESMA DIRETORIA FORA
diretoria externa:diretoria interna (docker)

docker run -d -itd -p 3838:3838 -v /srv/shinyapps:/srv/shiny-server -v /srv/shinylog:/var/log/shiny-server --name phdshiny rocker/shiny

docker run -itd -p 8787:8787 -e ROOT=TRUE -e PASSWORD=phdrisk -v /srv/shinyapps:/home/rstudio/shiny-server  --name phdrstudio phdriskdocker/phdrstudio:vxx

https://www.edivaldobrito.com.br/instalar-java-no-linux-veja-como-fazer-isso-manualmente/

no prompoy: apt update && apt upgrade && apt gedit ou nano

::: obs no rstudio deve-se instalar o sudo apt install default-jre


Passo 7. Se seu sistema é de 64 bits, use o comando abaixo para baixar o Java. Se o link estiver desatualizado, acesse essa página, baixe a última versão e salve-o com o nome jre-linux.tar.gz;

wget https://javadl.oracle.com/webapps/download/AutoDL?BundleId=241526_1f5b5a70bf22433b84d0e960903adac8 -O jre-linux.tar.gz


Passo 9. Depois de baixar, crie a pasta “jvm” em “/usr/lib” com o comando:

sudo mkdir /usr/lib/jvm

Passo 10. Execute o comando abaixo para descomprimir o pacote baixado, para a pasta criada;

sudo tar zxvf jre-linux.tar.gz -C /usr/lib/jvm

Passo 11. Renomeie a pasta criada. Se ao executar o comando abaixo ocorrer um erro com a mensagem iniciando com “mv: é impossível sobrescrever o não-diretório”, pule este passo;

sudo mv /usr/lib/jvm/jre*/ /usr/lib/jvm/jre

Passo 12. Crie um link simbólico para a pasta criada;

sudo ln -s /usr/lib/jvm/jre /usr/lib/jvm/java-oracle

Como configurar o ambiente Java no Linux manualmente

Para configurar o ambiente Java no Linux manualmente, faça o seguinte:

Passo 1. Crie uma cópia do arquivo /etc/profile;

sudo cp -a /etc/profile /etc/profile.original

Passo 2. Agora abra o arquivo com seu editor de texto favorito;

sudo gedit /etc/profile

Passo 3. Digite ou cole (recomendável) o texto abaixo dentro do arquivo, mais exatamente pouco depois das primeiras linhas (os comentários com símbolo # no inicio da linha). A seguir, salve e feche o arquivo;

JAVA_HOME=/usr/lib/jvm/java-oracle/
PATH=$JAVA_HOME/bin:$PATH export PATH JAVA_HOME
CLASSPATH=$JAVA_HOME/lib/tools.jar
CLASSPATH=.:$CLASSPATH
export  JAVA_HOME  PATH  CLASSPATH

reboot
# PACOTES
install.packages(
  c("shinydashboard","shinyalert","shinyjs","dplyr","ramdomForest",
    "ggthemes","formattable","DT","h2o"
  ))

# INSTALACOES NECESSARIAS
- devtools
- install_version(h2o, version=)

# UTEIS
## INSTALACAO COM DEPENDENCIAS UTILIZAR
- install_packages(pacote, dependencies=TRUE)

# instalar devtools shiny docker
- instalar libssl, libxml, libxml2-dev (linux)
- instalar xml (R)

# sincronizar o h20 nos dois apps
- install.packages("h2o", type="source", repos=(c("http://h2o-release.s3.amazonaws.com/h2o/latest_stable_R")))



# ENVIAR A PASTA DE ARQUIVOS (JUNTO - GAMBIARRA)
 - criar uma pasta fora da pasta "shiny-server", dentro do rstudio, no mesmo local da pasta "kitmatic": ex. arquivos/
 - copie a pasta de dentro do shiny-server. ex shiny-server/saude para essa pasta criada: ex. arquivos/saude
 - envie para o dockerhub
 - ao fazer pull da imagem, mova a pasta dentro de "arquivos/" para "shiny-server"
 
# ENVIAR ARQUIVO SHINYAPP.IO

 - https://shiny.rstudio.com/articles/shinyapps.html
 - https://www.shinyapps.io 
 - library(rsconnect)
 - setwd("~/shiny-server/bimarketing")

 - rsconnect::setAccountInfo(name='phdrisk',
                          token='D5E65BA5F2C8D5805E0D2C3B9970AA49',
                          secret='Kr9QXbHSfsbEqCU58HDsBbY1uWd6MXdyNr5cfF5b1960')

- rsconnect::deployApp("~/shiny-server/bimarketing")
- terminateApp("bimarketing")

# DICAS UTEIS
```
RenderPlot({ 
    # MENSAGEM QUANDO O PLOT ESTA INCOMPLETO
    validate(need(input$dataTableInfeccao_rows_selected, 'Por Favor, Selecione uma linha na tabela primeiro! ')  )
    })
```
# js 
```
jsReload <- "shinyjs.refresh = function() { location.reload(); }"

  library(shinyjs)
  shiny::shinyApp(
    ui = f7Page(
      shinyjs::useShinyjs(),
      shinyjs::extendShinyjs(text=jsReload, functions = "refresh"),
      ....
      shinyjs::js$refresh()
      
```

# CONFIGURAR ROTAS
```
 https://docs.rstudio.com/shiny-server/#redirecting
```

