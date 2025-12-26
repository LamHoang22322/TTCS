FROM nginx:alpine

# Xóa file mặc định của nginx
RUN rm -rf /usr/share/nginx/html/*

# Copy toàn bộ code HTML vào nginx
COPY . /usr/share/nginx/html

EXPOSE 80
