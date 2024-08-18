FROM python:3.8

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    build-essential \
    libsm6 \
    libxext6 \
    libxrender-dev \
    && rm -rf /var/lib/apt/lists/*

# Crear un directorio de trabajo
WORKDIR lab

# Instalar dependencias de Python
RUN pip install -U --force-reinstall --no-cache https://github.com/johnhw/jhwutils/zipball/master
RUN pip install scikit-image
RUN pip install -U --force-reinstall --no-cache https://github.com/AlbertS789/lautils/zipball/master
RUN pip install notebook
RUN pip install datasets nltk
RUN pip install -U torch==1.9.0+cu111 -f https://download.pytorch.org/whl/cu111/torch_stable.html
RUN pip install -U torchtext==0.10.0
RUN pip install spacy

# Instalar modelos de spaCy
RUN python -m spacy download de_core_news_sm
RUN python -m spacy download en_core_web_sm

RUN pip install --upgrade pip
RUN pip install ipywidgets

# Copiar el notebook al contenedor
COPY . .

# Exponer el puerto para Jupyter Notebook
EXPOSE 8811

# Comando para ejecutar Jupyter Notebook y mantener el contenedor corriendo
CMD ["sh", "-c", "jupyter notebook --ip=0.0.0.0 --port=8811 --no-browser --allow-root && tail -f /dev/null"]
