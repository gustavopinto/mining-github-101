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
	
  i = 0	

  for page in range(1, max_pages):
    print "Page: " + str(page)
    repo = "%s/%s?page=%s" % (project, type, page)
    forks = []

    try:
      forks = read_data(repo)
      print "Total pagina " + str(page) + ": " + str(len(forks))
			i += len(forks)

      for fork in forks:
        print fork['full_name']

    except NoMorePagesAvailable:
      sys.exit("We are done!!")
			print "Total of forks: " + str(i) 


period = gather_metadata("funcoeszz/funcoeszz", "forks")
```

## O que preciso instalar?

## Como devo rodar?

## O que o código faz?

## O que é esse api.github.com?
