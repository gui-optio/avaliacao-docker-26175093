# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Guilherme Melo Freitas
Matrícula: 26175093
Usuário do GitHub: gui-optio
Usuário do Docker Hub: guimelof

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
  nginx:1.28-alpine, e a imagem ficou com 25.8MB (91.7MB em disco).
2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
  conferir que o `index.html` está lá dentro.
   /usr/share/nginx/html
   docker exec teste-portal ls -l /usr/share/nginx/html

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
  guimelof/viaserra-portal:1.0-26175093
   [https://hub.docker.com/r/guimelof/viaserra-portal](https://hub.docker.com/r/guimelof/viaserra-portal)
4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
  Fazer o build de novo e depois o push:
   docker build -t guimelof/viaserra-portal:1.0-26175093 ./portal
   docker push guimelof/viaserra-portal:1.0-26175093

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.


| #   | Instrução                | O que estava errado                                              | O que você viu acontecer                      | Como corrigiu                                   |
| --- | ------------------------ | ---------------------------------------------------------------- | --------------------------------------------- | ----------------------------------------------- |
| 1   | COPY pagina/ .           | a pasta pagina não existe, o certo é site                        | o build deu erro "/pagina": not found         | troquei para COPY site/ .                       |
| 2   | CMD ["nginx"]            | faltava o daemon off, o nginx ia pro fundo e o container fechava | o container ficava Exited (0) no docker ps -a | troquei para CMD ["nginx", "-g", "daemon off;"] |
| 3   | WORKDIR /usr/share/nginx | a pasta certa é /usr/share/nginx/html                            | abria a página "Welcome to nginx!"            | troquei para WORKDIR /usr/share/nginx/html      |


6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
  O primeiro número é a porta do computador e o segundo é a do container. No 7042:80 funciona porque o nginx
   usa a porta 80. No 80:7042 não funciona porque não tem nada na 7042 do container. A porta do container é
   a da direita.

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
  docker run -d -p 8093:80 --restart unless-stopped guimelof/viaserra-portal:1.0-26175093
   docker run -d -p 7093:80 --restart unless-stopped manutencao:26175093
8. Qual comando derruba os dois containers de uma vez?
  docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:

```
VIASERRA-26175093-72416D4C
```

