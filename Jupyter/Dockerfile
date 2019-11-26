#Utilizando esta versão para os testes devido a compatibilidades com meu hardware, ótima versão por sinal
FROM ubuntu:19.04


# Update e Upgrade da imagem
RUN apt-get update && yes|apt-get upgrade
RUN apt-get install -y emacs

# Instalar wget, git, make, bzip2 e python3.5
RUN apt-get install -y wget bzip2
RUN apt-get install -y git
RUN apt-get install -y make
#RUN apt-get install -y python3.5
RUN apt-get install -y libzmq3-dev
RUN apt-get install -y python3-pip
RUN apt-get install -y python-dev python-numpy
RUN pip3 install --upgrade pip
# Instalar sudo
RUN apt-get install -y sudo

# Adicionar usuario ubuntu sem senha, adicionar para o grupo sudo
RUN adduser --disabled-password --gecos '' ubuntu
RUN adduser ubuntu sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER ubuntu
WORKDIR /home/ubuntu/
RUN chmod a+rwx /home/ubuntu/

# Instalar Anaconda 
RUN wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
RUN bash Anaconda3-5.0.1-Linux-x86_64.sh -b
RUN rm Anaconda3-5.0.1-Linux-x86_64.sh

# Setar path para o conda
ENV PATH /home/ubuntu/anaconda3/bin:$PATH

# Updatie nos pacotes do Anaconda
RUN conda update conda
#RUN conda update anaconda
#RUN conda update --all
RUN pip3 install --user numpy
RUN pip  install --user opencv-contrib-python
RUN conda install -c pytorch magma-cuda101 torchvision
# Configuriar accesso ao Jupyter
RUN mkdir /home/ubuntu/notebooks
RUN jupyter notebook --generate-config --allow-root
RUN echo "c.NotebookApp.password = u'sha1:6a3f528eec40:6e896b6e4828f525a6e20e5411cd1c8075d68619'" >> /home/ubuntu/.jupyter/jupyter_notebook_config.py

# Travar porta do Jupyter port: 8888
EXPOSE 8888

CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/home/ubuntu/notebooks", "--ip='*'", "--port=8888", "--no-browser"]

