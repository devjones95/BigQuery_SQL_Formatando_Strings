Funções de Texto no SQL

Este repositório contém exemplos práticos de manipulação de textos em SQL utilizando BigQuery. Abaixo estão algumas funções essenciais para trabalhar com strings.

CONCAT

Concatena valores de colunas ou strings literais.

SELECT
  "Olá",
  "Mundo",
CONCAT("Olá" ", " "mundo");


SELECT 
  id, 
  first_name,
  last_name,
  CONCAT(first_name, ' ', last_name) AS nome_completo
FROM bigquery-public-data.thelook_ecommerce.users;


SELECT o.order_id,
CONCAT('Quantidade total de intens no pedido: ', AVG(o.num_of_item), ' - ', 'Receita total do pedido: ', ROUND(SUM(sale_price), 2)) AS detalhe

FROM bigquery-public-data.thelook_ecommerce.orders AS o
JOIN bigquery-public-data.thelook_ecommerce.order_items AS oi
  ON o.order_id = oi.order_id

GROUP BY 1
ORDER BY 1;

 <hr>

STARTS_WITH

Filtra valores que começam com determinada string.

SELECT
  id,
  first_name
FROM bigquery-public-data.thelook_ecommerce.users

WHERE STARTS_WITH(first_name, 'Mi') IS TRUE; -- IS TRUE nesse caso é opcional

<hr>

LOWER e UPPER

Converte strings para letras minúsculas ou maiúsculas.

SELECT DISTINCT
  repo_name AS lower_repo_name

FROM bigquery-public-data.github_repos.sample_repos

WHERE LOWER(repo_name) LIKE '%python%';



SELECT DISTINCT
  repo_name AS upper_repo_name

FROM bigquery-public-data.github_repos.sample_repos

WHERE UPPER(repo_name) LIKE '%PYTHON%';

<hr>

INITCAP

Transforma a primeira letra de cada palavra em maiúscula.

SELECT 
  id, 
  first_name,
  last_name,
  CONCAT(first_name, ' ', last_name) AS nome_completo,
  LOWER(CONCAT(first_name, ' ', last_name)) AS nome_completo_1,
  UPPER(CONCAT(first_name, ' ', last_name)) AS nome_completo_2,
  INITCAP(CONCAT(first_name, ' ', last_name)) AS nome_completo_3
FROM bigquery-public-data.thelook_ecommerce.users;

<hr>

SPLIT

Separa uma string com base em um delimitador.

SELECT
  SPLIT('Por favor, parem de atribuir a mim as frases que eu nunca pronunciei - Albert Einstein', ' ') AS PALAVRAS; -- o delimitador do split no caso está sendo o espaço ' '.

<hr>

TRIM

Remove espaços ou caracteres especificados do início e/ou fim de uma string.

SELECT
  TRIM('CPF: 123.456.789-0', 'CPF: ') -- primeiro selecionamos onde queremos tirar, em seguida, o que queremos tirar
  LTRIM('CPF: 123.456.789-0', 'CPF: ') -- esquerda
  RTRIM('CPF: 123.456.789-0', 'CPF: '); -- direita

  




