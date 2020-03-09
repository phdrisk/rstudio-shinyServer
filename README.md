
# DOCKER ( SHINY E RSTUDIO) - UTILIZANDO MESMA DIRETORIA FORA
diretoria externa:diretoria interna (docker)
docker run -d -itd -p 3838:3838 -v /srv/shinyapps/:/srv/shiny-server/ -v /srv/shinylog/:/var/log/shiny-server/ --name phdshiny rocker/shiny

docker run -itd -p 8787:8787 -e PASSWORD=phdrisk -v /srv/shinyapps/:/home/rstudio/shiny-server  --name phdrstudio rocker/rstudio

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
  c("shinydashboard","shinyalert","shinyjs","dplyr","ramdomForeste",
    "ggthemes","formattable","DT","h2o"
  ))

