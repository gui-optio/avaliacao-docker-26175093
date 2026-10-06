# Portal ViaSerra Transportes - site estatico servido pelo Nginx
FROM nginx:1.28-alpine

LABEL autor="Guilherme Melo Freitas" \
      matricula="26175093" \
      descricao="Portal da ViaSerra Transportes"

# o Nginx serve os arquivos a partir de /usr/share/nginx/html
COPY html/ /usr/share/nginx/html/

EXPOSE 80
