# Análise Integrada dos Dados de Acidentes, Tipos de Veículos e Vítimas

Este projeto reúne e organiza de forma unificada as análises dos dados de acidentes, tipos de veículos e vítimas do município de São Paulo, utilizando a base RENAEST.

## Como executar

### 1. Pré-requisitos

- Python 3.8 ou superior
- Recomenda-se o uso de um ambiente virtual (venv, conda, etc)
- Jupyter Notebook ou VS Code com suporte a notebooks

### 2. Instalação das dependências

Execute no terminal ou adicione a célula abaixo no início do notebook:

```python
%pip install pandas matplotlib seaborn numpy requests
```

Ou, se preferir, use o arquivo `requirements.txt`:

```
pandas
matplotlib
seaborn
numpy
requests
```

E instale com:

```
pip install -r requirements.txt
```

### 3. Download e extração automática dos dados

O notebook já possui uma célula que faz o download e a extração dos dados diretamente do portal do governo, usando apenas Python puro (compatível com Windows, Linux e Mac):

```python
import requests
import zipfile
import os

link = "https://dados.transportes.gov.br/dataset/42e2320b-ea67-4fdc-896f-71363e043fc6/resource/5f33e23b-bdd8-48bd-b267-27532ba22912/download/renaest_dabertos_20250412.zip"
zip_path = "dataset.zip"
extract_dir = "dataset"

with requests.get(link, stream=True) as r:
    r.raise_for_status()
    with open(zip_path, "wb") as f:
        for chunk in r.iter_content(chunk_size=8192):
            f.write(chunk)

with zipfile.ZipFile(zip_path, "r") as zip_ref:
    zip_ref.extractall(extract_dir)

os.remove(zip_path)
print(os.listdir(extract_dir))
```

### 4. Estrutura esperada das pastas

Após a extração, os arquivos CSV estarão em:

```
dataset/renaest_dabertos_20250412/
```

### 5. Execução das análises

Basta seguir as células do notebook `analise_refatorada.ipynb`.  
As análises incluem:

- Limpeza e filtragem dos dados
- Integração dos datasets
- Análises estatísticas e geração de gráficos
- Análise demográfica das vítimas

### 6. Observações

- Não utilize comandos de sistema operacional (`wget`, `ls`, `rm`, etc). Todo o processo é feito em Python puro.
- Caso algum pacote não seja encontrado, instale usando `%pip install nome_do_pacote` em uma célula do notebook.

---

**Autor:**  
Frederico Amaral Júnior

**Licença:**
