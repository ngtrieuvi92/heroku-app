FROM appsmith/appsmith-editor as frontend

FROM appsmith/appsmith-server

RUN mkdir -p /var/www/appsmith
COPY --from=appsmith/appsmith-editor /var/www/appsmith /var/www/appsmith

RUN apk add --update nginx && \ 
				rm -rf /var/cache/apk/* && \
				mkdir -p /tmp/nginx/client-body && \
				apk --no-cache add gettext bash curl

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf.template /etc/nginx/conf.d/default.conf.template
COPY bootstrap.sh /bootstrap.sh
COPY integromat.sh /integromat.sh
RUN chmod +x /integromat.sh

EXPOSE 80

ENTRYPOINT [ "/bin/bash" ]
CMD ["/bootstrap.sh"]

