## Primeiro exemplo: Baixando forks

Nesse primeiro exemplo, vamos baixar todos os forks de um projeto. O projeto, no caso, é a ``funcoeszz``. Ao fim da execução, os nomes dos forks da ``funcoeszz`` serão impressos no terminal.

```python
import json, requests, sys

class NoMorePagesAvailable(Exception):
  pass

def read_data(repo):
  url = "https://api.github.com/repos/" + repo

  resp = requests.get(url)

  if len(resp.text) == 2:
    raise NoMorePagesAvailable()
  else:
    forks = json.loads(resp.text)
    return forks

def gather_metadata(project, type):
  max_pages = 10000000 # limite de paginas da api do github

  for page in range(1, max_pages):
    print "Page: " + str(page)
    repo = "%s/%s?page=%s" % (project, type, page)
    forks = []

    try:
      forks = read_data(repo)
      print "Total pagina " + str(page) + ": " + str(len(forks))

      for fork in forks:
        print fork['full_name']

    except NoMorePagesAvailable:
      sys.exit("We are done!!") 


period = gather_metadata("funcoeszz/funcoeszz", "forks")
```

## O que preciso instalar?
Para poder rodar o código acima e outros em python (\*.py), é necessário antes instalar o python.
No Linux: Entre no terminal e digite `sudo apt install python` ou `sudo apt-get install python` e aguarde o término da instalação. Instale também o pip, digitando `sudo apt install python-pip`, para gerenciar os pacotes que os códigos em python podem importar. Depois, faça o *upgrade* do pip, digitando `sudo -H pip install --upgrade pip` e aguarde a atualização acontecer.

## Como devo rodar?
Crie no terminal um arquivo (pode ser com o nano, o gedit, ou outros) e salve com formatação py e um nome, de preferência sem espaços. Copie tudo e cole neste arquivose salve. Vá no prompt IDLE do Python ou no terminal e digite: `python nome_do_arquivo.py` e tecle ENTER, ele deve funcionar bem.

## O que o código faz?
Acessa os forks da página <https://github.com/funcoeszz/funcoeszz> e lista cada um deles de acordo com as suas páginas, escrevendo o total de forks em cada uma dessas páginas.

## O que é esse api.github.com?
