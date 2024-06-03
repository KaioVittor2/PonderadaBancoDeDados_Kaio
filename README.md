# Ponderada Banco De Dados _ Kaio

Banco de dados:

![alt text](assets/Tabela_foto.png)

Explicação da tabela: 

**Tabela 'users'**
- Armazena informações sobre os usuários do sistema.
- Cada registro representa um usuário e contém detalhes como nome, idade, gênero, email, senha, localização, entre outros.
- O campo "id" é a chave primária.
- O campo "followers" armazena o número de seguidores que o usuário possui.

**Tabela 'posts'**
- Responsável por armazenar as postagens feitas pelos usuários.
- Cada registro corresponde a uma postagem e inclui informações como o conteúdo da postagem, número de curtidas e uma referência ao usuário que fez a postagem.
- O campo "id_users" é uma chave estrangeira que relaciona cada postagem ao usuário que a fez.

**Tabela 'preferences'**
- Registra as preferências de cada usuário em relação a determinadas ações e público-alvo.
- Cada registro associa um usuário a uma preferência específica, representada pelo campo "id_actions_and_target_public".

**Tabela 'actions_and_target_public'**
- Contém uma lista de ações possíveis e públicos-alvo para as preferências dos usuários.
- Cada registro define uma ação e o público-alvo associado a essa ação.

**Tabela 'posts_actions_and_target_public'**
- Estabelece a relação entre postagens, ações e público-alvo.
- Registra quais ações foram realizadas em cada postagem e qual público-alvo está associado a essas ações.

**Tabela 'Friends_view'**
- Mantém uma visualização das interações entre usuários e suas postagens.
- Cada registro representa uma interação entre um usuário e uma postagem,
  como uma visualização de amigo.
- As chaves estrangeiras "id_users" e "id_Posts" relacionam o usuário e a postagem envolvidos na interação.


<br><br>
Código SQL
<br><br>
-- Globals
-- ---

-- SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";
-- SET FOREIGN_KEY_CHECKS=0;

-- ---
-- Table 'users'
-- 
-- ---

DROP TABLE IF EXISTS users;
		
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(50),
  age INT,
  gender VARCHAR(20),
  type BYTEA,
  email VARCHAR,
  password INT,
  location VARCHAR(50),
  "new field" INTEGER,
  followers INT
);

-- ---
-- Table 'posts'
-- 
-- ---

DROP TABLE IF EXISTS posts;
		
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  id_users INT,
  image BYTEA,
  content VARCHAR(400),
  likes INTEGER
);

-- ---
-- Table 'preferences'
-- 
-- ---

DROP TABLE IF EXISTS preferences;
		
CREATE TABLE preferences (
  id SERIAL PRIMARY KEY,
  id_users INT,
  id_actions_and_target_public INT
);

-- ---
-- Table 'actions_and_target_public'
-- 
-- ---

DROP TABLE IF EXISTS actions_and_target_public;
		
CREATE TABLE actions_and_target_public (
  id SERIAL PRIMARY KEY,
  actions VARCHAR(20),
  target_public VARCHAR(20)
);

-- ---
-- Table 'posts_actions_and_target_public'
-- 
-- ---

DROP TABLE IF EXISTS posts_actions_and_target_public;
		
CREATE TABLE posts_actions_and_target_public (
  id SERIAL PRIMARY KEY,
  id_posts INT,
  id_actions_and_target_public INT
);

-- ---
-- Table 'Friends_view'
-- 
-- ---

DROP TABLE IF EXISTS Friends_view;
		
CREATE TABLE Friends_view (
  id SERIAL PRIMARY KEY,
  id_users INT,
  id_Posts INT
);

-- ---
-- Foreign Keys 
-- ---

ALTER TABLE posts ADD CONSTRAINT fk_posts_users FOREIGN KEY (id_users) REFERENCES users (id);
ALTER TABLE preferences ADD CONSTRAINT fk_preferences_users FOREIGN KEY (id_users) REFERENCES users (id);
ALTER TABLE preferences ADD CONSTRAINT fk_preferences_actions_and_target_public FOREIGN KEY (id_actions_and_target_public) REFERENCES actions_and_target_public (id);
ALTER TABLE posts_actions_and_target_public ADD CONSTRAINT fk_posts_actions_and_target_public_posts FOREIGN KEY (id_posts) REFERENCES posts (id);
ALTER TABLE posts_actions_and_target_public ADD CONSTRAINT fk_posts_actions_and_target_public_actions_and_target_public FOREIGN KEY (id_actions_and_target_public) REFERENCES actions_and_target_public (id);
ALTER TABLE Friends_view ADD CONSTRAINT fk_Friends_view_users FOREIGN KEY (id_users) REFERENCES users (id);
ALTER TABLE Friends_view ADD CONSTRAINT fk_Friends_view_posts FOREIGN KEY (id_Posts) REFERENCES posts (id);

-- ---
-- Test Data
-- ---

-- INSERT INTO users (name, age, gender, type, email, password, location, "new field", followers) VALUES
-- ('', NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL);
-- INSERT INTO posts (id_users, image, content, likes) VALUES
-- (NULL, NULL, NULL, NULL);
-- INSERT INTO preferences (id_users, id_actions_and_target_public) VALUES
-- (NULL, NULL);
-- INSERT INTO actions_and_target_public (actions, target_public) VALUES
-- (NULL, NULL);
-- INSERT INTO posts_actions_and_target_public (id_posts, id_actions_and_target_public) VALUES
-- (NULL, NULL);
-- INSERT INTO Friends_view (id_users, id_Posts) VALUES
-- (NULL, NULL);