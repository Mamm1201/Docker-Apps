FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

# Configura npm para ignorar errores de certificados autofirmados
RUN npm config set strict-ssl false \
    && npm config set registry https://registry.npmjs.org/ \
    && npm install

COPY . .

RUN npm run build

# etapa 2 servir archivos
FROM nginx:stable-alpine

COPY --from=builder /app/dist /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d

EXPOSE 80

CMD ["nginx","-g","daemon off;"]



