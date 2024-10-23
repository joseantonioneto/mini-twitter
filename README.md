# Projeto mini-twitter

### Este projeto é uma API construída com Django e Django REST Framework (DRF), com autenticação baseada em **JSON Web Tokens (JWT)** e suporte à paginação para uma lista de posts.


## 📚 Tecnologias Utilizadas

-   [Django](https://www.djangoproject.com/)
-   [Django REST Framework](https://www.django-rest-framework.org/)
-   [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/)


Este projeto é uma API construída com Django e Django REST Framework (DRF), com autenticação baseada em **JSON Web Tokens (JWT)** e suporte à paginação para uma lista de posts.

## 🛠 Funcionalidades

-   CRUD completo para posts (Create, Read, Update, Delete).
-   Autenticação de usuários usando **JWT**.
-   Paginação implementada para listas de posts.
-   Design baseado em princípios RESTful.

## 🚀 Instalação e Configuração

### Pré-requisitos

Certifique-se de ter o Python 3.8+ e o Git instalados na sua máquina.

### Passo a Passo

1.  **Clone o repositório:**
    ```
    git clone https://github.com/joseantonioneto/mini-twitter.git
    cd mini-twitter
    ```
    
2.  **Crie um ambiente virtual:**
    
	 ```
	python -m venv env
	source env/bin/activate # Linux/MacOS 
	env\Scripts\activate # Windows 
	```

3.  **Instale as dependências:**
    
  
	   ```
	   pip install django djangorestframework djangorestframework-simplejwt 
	  ```
    
4.  **Aplique as migrações:**
	```
	python manage.py migrate
	```
5.  **Crie um superusuário (opcional):**
    ```
    python manage.py createsuperuser
    ```
6.  **Execute o servidor de desenvolvimento:**
    ```
    python manage.py runserver
    ```

Agora, a API estará disponível em `http://127.0.0.1:8000/`.

## 🔑 Autenticação

A API usa **JWT (JSON Web Tokens)** para autenticação. Para obter um token de acesso e refrescar, siga os passos abaixo:

1.  **Obtenha o Token de Acesso e Refresh:**
    
    Faça uma requisição `POST` para o endpoint `/api/token/` com as credenciais de um usuário existente:
    
    -   **Endpoint:** `POST /api/token/`
        
    -   **Corpo da requisição:**
        
        json
        
        Copiar código
        
        `{
          "username": "your_username",
          "password": "your_password"
        }` 
        
    -   **Resposta de sucesso:**
        
        json
        
        Copiar código
        
        `{
          "refresh": "<refresh_token>",
          "access": "<access_token>"
        }` 
        
2.  **Acessar Recursos Autenticados:**
    
    Para acessar os endpoints que requerem autenticação, envie o token de acesso no cabeçalho da requisição:
    
    plaintext
    
    Copiar código
    
    `Authorization: Bearer <access_token>` 
    
3.  **Renovar o Token de Acesso:**
    
    Quando o token de acesso expirar, você pode usar o **refresh token** para obter um novo token de acesso enviando uma requisição `POST` para o endpoint `/api/token/refresh/`:
    
    -   **Endpoint:** `POST /api/token/refresh/`
        
    -   **Corpo da requisição:**
        
        json
        
        Copiar código
        
        `{
          "refresh": "<refresh_token>"
        }` 
        
    -   **Resposta de sucesso:**
        
        json
        
        Copiar código
        
        `{
          "access": "<new_access_token>"
        }` 
        

## 📄 Endpoints

### Listar e Criar Posts

-   **Endpoint:** `GET/POST /api/posts/`
-   **Autenticação:** Necessária para todos os métodos.
-   **Descrição:**
    -   `GET` retorna uma lista paginada de posts.
    -   `POST` cria um novo post (necessário envio de dados no corpo).

Exemplo de requisição para criar um post:

json

Copiar código

`{
  "title": "Meu Post",
  "content": "Conteúdo do meu post",
  "author": "Nome do autor"
}` 

### Paginação

Ao listar posts, a resposta será paginada. O tamanho da página é definido por padrão para **10 itens por página**. Exemplo de resposta paginada:

json

Copiar código

`{
   "count": 50,
   "next": "http://127.0.0.1:8000/api/posts/?page=2",
   "previous": null,
   "results": [
       {
           "id": 1,
           "title": "Post 1",
           "content": "Conteúdo do primeiro post",
           "author": "Autor 1",
           "created_at": "2024-10-23T10:00:00Z"
       },
       ...
   ]
}` 
