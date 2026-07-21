FROM nginx:1.24.0

#removing default content nginx/html and nginx.conf and default.conf
RUN rm -rf /usr/share/nginx/html/* 
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf

# copying static files into /usr/share/nginx/html/ and nginx.conf into /etc/nginx/nginx.conf
COPY static/ /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/nginx.conf