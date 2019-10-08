# How to install Leptonica, Opencv 3.2 and Tesseract 4

:star::star::star::star::star:

### Install python c++ opencv from learnopencv

https://www.learnopencv.com/install-opencv3-on-ubuntu/

### Update packages


```
sudo apt-get update
sudo apt-get upgrade
```

### Install OS libraries

```
Remove any previous installations of x264</h3>
sudo apt-get remove x264 libx264-dev
 
We will Install dependencies now
 
sudo apt-get install build-essential checkinstall cmake pkg-config yasm
sudo apt-get install git gfortran
sudo apt-get install libjpeg8-dev libjasper-dev libpng12-dev
 
# If you are using Ubuntu 14.04
sudo apt-get install libtiff4-dev
# If you are using Ubuntu 16.04
sudo apt-get install libtiff5-dev
 
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev
sudo apt-get install libxine2-dev libv4l-dev
sudo apt-get install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev
sudo apt-get install qt5-default libgtk2.0-dev libtbb-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libfaac-dev libmp3lame-dev libtheora-dev
sudo apt-get install libvorbis-dev libxvidcore-dev
sudo apt-get install libopencore-amrnb-dev libopencore-amrwb-dev
sudo apt-get install x264 v4l-utils
 
# Optional dependencies
sudo apt-get install libprotobuf-dev protobuf-compiler
sudo apt-get install libgoogle-glog-dev libgflags-dev
sudo apt-get install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen
```

### Install Python libraries

```
sudo apt-get install python-pip
sudo apt-get install python3-pip

# Install virtual environment
sudo pip2 install virtualenv virtualenvwrapper
sudo pip3 install virtualenv virtualenvwrapper
echo "# Virtual Environment Wrapper"  >> ~/.bashrc
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
source ~/.bashrc
  
############ For Python 2 ############
# create virtual environment
mkvirtualenv facecourse-py2 -p python2
workon facecourse-py2
  
# now install python libraries within this virtual environment
pip install numpy scipy matplotlib scikit-image scikit-learn ipython
  
# quit virtual environment
deactivate
######################################
  
############ For Python 3 ############
# create virtual environment
mkvirtualenv facecourse-py3 -p python3
workon facecourse-py3
  
# now install python libraries within this virtual environment
pip install numpy scipy matplotlib scikit-image scikit-learn ipython
  
# quit virtual environment
deactivate
######################################
```

### Configure compiling environment
```
sudo pip install cython
```

### Upgrade g++5
```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
```

### Install dependency packages

```
sudo apt-get install -y autoconf automake libtool
sudo apt-get install -y autoconf-archive

sudo apt-get install -y pkg-config

sudo apt-get install -y libpng12-dev
sudo apt-get install -y libjpeg8-dev
sudo apt-get install -y libtiff5-dev

sudo apt-get install -y zlib1g-dev
sudo apt-get install -y libicu-dev

sudo apt-get install -y libpango1.0-dev
sudo apt-get install -y libcairo2-dev
```

### Install Leptonica 1.74
#### Install it from source code

1. Download the source code from [Leptonica](http://www.leptonica.com/download.html).

2. Following the instructions to install it, extract it:

```
cd leptonica-1.76.0

sudo ./configure

sudo make -j8 (8 is the number of cores, change it if necessary)
sudo make install
sudo ldconfig
```
### Find "cv2*.so"

```
find /usr/local/lib/ -type f -name "cv2*.so"

############ For Python 2 ############
## binary installed in dist-packages
/usr/local/lib/python2.6/dist-packages/cv2.so
/usr/local/lib/python2.7/dist-packages/cv2.so

## binary installed in site-packages
/usr/local/lib/python2.6/site-packages/cv2.so
/usr/local/lib/python2.7/site-packages/cv2.so
  
############ For Python 3 ############
## binary installed in dist-packages
/usr/local/lib/python3.5/dist-packages/cv2.cpython-35m-x86_64-linux-gnu.so
/usr/local/lib/python3.6/dist-packages/cv2.cpython-36m-x86_64-linux-gnu.so

## binary installed in site-packages
/usr/local/lib/python3.5/site-packages/cv2.cpython-35m-x86_64-linux-gnu.so
/usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so
```


### Install Tesseract 4.0

1. Clone the [repository from Github](https://github.com/tesseract-ocr/tesseract):

2. Compiling it and install it.

```
cd tesseract-master

sudo sh autogen.sh
sudo ./configure

LDFLAGS="-L/usr/local/lib" CFLAGS="-I/usr/local/include"

sudo make -j8
sudo make install 
sudo make install -langs
sudo make training
sudo make training-install

export LD_LIBRARY_PATH=/usr/local/lib
```
### Update ~/.bashrc

```
gedit ~/.bashrc
```

Concatenar ao final do arquivo: 
```
export TESSDATA_PREFIX=<YOUR PATH>/tesseract-master/tessdata 
```

(salve o arquivo).

```
source ~/.bashrc
sudo ldconfig
```

### Install Opencv

```
cd ~

sudo apt-get update
sudo apt-get upgrade

sudo apt-get install build-essential cmake pkg-config
sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev

sudo apt-get install libatlas-base-dev gfortran

wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip 
unzip opencv.zip

wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
unzip opencv_contrib.zip

wget https://bootstrap.pypa.io/get-pip.py

sudo python get-pip.py
sudo pip install virtualenv virtualenvwrapper
sudo rm -rf ~/get-pip.py ~/.cache/pip
```

### Update ~/.bashrc

```
gedit ~/.bashrc
```

Add in the end of file:
```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```

```
source ~/.bashrc
mkvirtualenv cv -p python3
sudo pip install numpy
```

##### Update /usr/local/include/tesseract/unichar.h 

```
sudo gedit /usr/local/include/tesseract/unichar.h	
```

Se necessário, coloque “std::” before “string” in the line 164.

### Compile and Install

```
cd opencv-3.2.0/

mkdir build

cd build
```

```
cmake -D CMAKE_BUILD_TYPE=RELEASE       -D CMAKE_INSTALL_PREFIX=/usr/local       -D INSTALL_C_EXAMPLES=ON       -D INSTALL_PYTHON_EXAMPLES=ON       -D WITH_TBB=ON       -D WITH_V4L=ON       -D WITH_QT=ON       -D WITH_OPENGL=ON       -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.2.0/modules       -D BUILD_EXAMPLES=ON .. 
```

OBS: Caso algo dê errado, você pode usar a flag `--ignore-errors`, para qualquer etapa.

```
# find out number of CPU cores in your machine
nproc
# substitute 4 by output of nproc
make -j4
sudo make install
sudo sh -c 'echo "/usr/local/lib" >> /etc/ld.so.conf.d/opencv.conf'
sudo ldconfig
```

### Create symlink in virtual environment

```
############ For Python 2 ############
cd ~/.virtualenvs/facecourse-py2/lib/python2.7/site-packages
ln -s /usr/local/lib/python2.7/dist-packages/cv2.so cv2.so
  
############ For Python 3 ############
cd ~/.virtualenvs/facecourse-py3/lib/python3.6/site-packages
ln -s /usr/local/lib/python3.6/dist-packages/cv2.cpython-36m-x86_64-linux-gnu.so cv2.so
```

### Test the OpenCV

Download this repository, then unzip RedEyeRemover.zip

```

```

### Update the files .traineddata

Para melhor desempenho, é necessário substituir os arquivos traineddata antigos pelas correspondentes versões referentes ao Tesseract 4.  
Estes podem ser baixados por aqui: https://github.com/tesseract-ocr/tessdata

### Adicionando uma nova fonte

Para adicionar uma fonte no Ubuntu, copie sua fonte para:
* /usr/share/fonts/truetype/

Você pode usar este comando para copiá-lo: 
```
sudo mv sua_fonte.ttf  /usr/share/fonts/truetype/
```

Para instalar fontes latinas: 
```
sudo apt-get install fonts-dejavu gsfonts ttf-mscorefonts-installer
```

Para saber o nome da sua fonte execute o comando: 
```
text2image --fonts_dir /usr/share/fonts --list_available_fonts
```

### Treinando uma fonte

Source: https://github.com/tesseract-ocr/tesseract/wiki/TrainingTesseract-4.00

#### Langdata
Para treinarmos uma nova fonte no tesseract 4, é necessário baixar o pacote langdata e colar no mesmo diretório do tesseract-master.
Haverá uma pasta com o nome do idioma que você quer treinar. Nela existe um arquivo com a extensão .training_text. Abra este arquivo e o edite. Coloque palavras e símbolos que estão contidos no documento que você quer treinar. Por exemplo: 

> REPÚBLICA 0123456789 FEDERATIVA DO BRASIL MINISTERIO CIDADES 
> NOME DOC. IDENTIDADE /
> OR.G EMISSOR / UF CPF DATA 0123456789 NASCIMENTO 660.007.851-00 0123456789 FILIAÇÃO
> PERMISSÃO ACC CAT CALIDADE REGISTRO 0123456789 HABILITAÇÃO CAT.HAB DOC. CPF DATA
> NASCIMENTO NOME ASSINATURA DETRAN PARAIBA SAO PAULO GOIAS DEPARTAMENTO NACIONAL DE TRANSITO CARTEIRA NASCIONAL DE HABILITAÇÃO CPF NASCIMENTO DATA FGHJKQUVXZ / - . , ; 0123456789 R$

OBSERVAÇÃO: Evite deixar a linha de texto muito comprida, pois isso pode acarretar ao erro Image not trainable, durante a etapa de fine tuning.

### Traineddata

Após isso, você deve baixar o traineddata que deseja treinar. Este se encontra aqui. Cole o arquivo .traineddata que você escolheu na pasta tesseract-master/tessdata. Caso você escolha alguma variação da linguagem, como por exemplo: por (default), por fast ou por best, apenas substitua o traineddata existente.

OBSERVAÇÃO: é necessário baixar o eng.traineddata e colar em tesseract-master/tessdata. Você encontra-o aqui.

### Trainamento

OBSERVAÇÃO: Algumas pastas podem vir com nomes um pouco diferente. Exemplo: A pasta tessdata pode estar escrito como tessdata-master. É só adaptar os comandos para o nome correto da pasta.

Os comandos abaixo irão treinar a sua fonte e salvar o resultado como um arquivo traineddata. É necessário editar algumas tags que estão presentes nos comandos:
	
<lang> deve ser substituído pelo nome da linguagem que você deseja treinar. Exemplos: por, eng, por_fast, por_best etc.

<font> deve ser substituído pelo nome da fonte que você deseja treinar. Para saber o nome da sua fonte execute o comando: text2image --fonts_dir /usr/share/fonts --list_available_fonts
Este comando irá listar todas as fontes instaladas em seu computador.
OBS: se necessário, instale o programa text2image.

Train:
```
chmod +x tesstrain.sh
training/tesstrain.sh --fonts_dir /usr/share/fonts --lang <lang> --linedata_only   --noextract_font_properties --langdata_dir ../langdata   --tessdata_dir ../tessdata --output_dir ~/tesstutorial/<lang>_train --fontlist "<font>" 
(também ajustar o caminho para tessdata e langdata, se necessário)
```

OBSERVAÇÃO 1: Você pode treinar com mais de uma fonte ao mesmo tempo, passando as fonte no parâmetro --fontlist, Exemplo: --fontlist "<font>" “<font>”.

OBSERVAÇÃO 2: caso seja retornado um erro semelhante a “ERROR: /tmp/tmp.j48OEyDg92/por/por.Arial_Bold.exp0.box não existe ou não é possível ler”: 
É possível que a fonte passada como parâmetro em --fontlist, ou não foi instalada, ou ela está com o seu nome diferente. 
Ou que na pasta tessdata esteja faltando eng.traineddata e/ou o seu .traineddata escolhido.

Eval:
```
training/tesstrain.sh --fonts_dir /usr/share/fonts --lang <lang> --linedata_only   --noextract_font_properties --langdata_dir ../langdata   --tessdata_dir ./tessdata   --fontlist "<font>" --output_dir ~/tesstutorial/<lang>_eval
```

OBSERVAÇÃO 3: Você pode treinar com mais de uma fonte ao mesmo tempo, passando as fonte no parâmetro --fontlist, Exemplo: --fontlist "<font>" “<font>”.

Fine tuning:
```
sudo mkdir -p ~/tesstutorial/<font>
sudo training/combine_tessdata -e tessdata/<lang>.traineddata   ~/tesstutorial/<font>/<lang>.lstm
sudo training/lstmtraining --model_output ~/tesstutorial/<font>/<font>   --continue_from ~/tesstutorial/<font>/<lang>.lstm   --traineddata tessdata/<lang>.traineddata   --train_listfile ~/tesstutorial/<lang>_eval/<lang>.training_files.txt   --max_iterations 400
```

OBSERVAÇÃO 4: É recomendado que você troque o parâmetro --max_iterations 400 por --target_error_rate 0

Combine the output files:
```
training/lstmtraining --stop_training --continue_from ~/tesstutorial/<font>/<font>_checkpoint --traineddata ~/tesseract-master/tessdata/<lang>.traineddata --model_output ~/tesstutorial/<lang>.traineddata
```

OBSERVAÇÃO 5: Caso retorne o seguinte erro: “Omgr_.Init(traineddata_path.c_str()):Error:Assert failed:in file ../lstm/lstmtrainer.h, line 110 Segmentation fault (core dumped)”, é provável que você esteja passando o .traineddata errado, ou o caminho para ele esteja errado. Verifique este parâmetro: ~/tesseract-master/tessdata/<lang>.traineddata, pois <lang>.traineddata deve ser o mesmo que você usou desde o início.

Pronto! O seu arquivo traineddata estará salvo aqui: ~/tesstutorial/<lang>.traineddata
	
