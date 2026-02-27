ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

# 1. 安装安装脚本
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

# 2. 安装常用工具 (可选)
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# 2. 定义扩展参数 (没有默认值，强制在 compose 中定义)
ARG PHP_EXTENSIONS

# 3. 安装扩展
# 这里的 ${PHP_EXTENSIONS} 会被替换成你在 docker-compose.yml 里写的字符串
RUN if [ -z "$PHP_EXTENSIONS" ]; then \
      echo "No extensions to install"; \
    else \
      install-php-extensions ${PHP_EXTENSIONS}; \
    fi

# 4. 为了兼容旧的 Nginx 配置习惯，我们在容器里创建 /home/wwwroot 目录
#    并设置正确的权限
RUN mkdir -p /home/wwwroot \
    && chown -R www-data:www-data /home/wwwroot \
    && chmod -R 755 /home/wwwroot

# 5. 切换到非 root 用户 www-data
# USER www-data

# 6. 设置工作目录
WORKDIR /home/wwwroot

# 启动
CMD ["php-fpm"]