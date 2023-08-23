"# Git Course"
1 – Foi realizado tratamento dos dados utilizando Banco de Dados SQL SERVER pois fica mais eficiente, pois a base de dados contém muita informação.
2 – Na tabela de resultados foram excluídas algumas colunas já que não seriam necessárias para os insights que iriamos obter.
3 – Na tabela perfil_eleitorado também foram excluídas algumas colunas igualmente com a tabela resultado.
4 – Após fazer o tratamento dos dados no SQL, importei os dados para o excel para construir uma tabela dinâmica, para visualizar os insights.
importCSV
SELECT*
FROM resultado2020;
alter table resultado2020
drop column QT_ELEITORES_BIOMETRIA_NH,
DT_ENCERRAMENTO,
DT_ABERTURA,
DS_CARGO_PERGUNTA_SECAO,
DT_CARGA_URNA_EFETIVADA,
CD_FLASHCARD_URNA_EFETIVADA,
CD_CARGA_2_URNA_EFETIVADA,
CD_CARGA_1_URNA_EFETIVADA,
NR_URNA_EFETIVADA;
select*
from INFORMATION_SCHEMA.TABLES
select top 2 percent* from resultado2020
select* from resultado2020
where NM_MUNICIPIO like 'SÃO%_'
-- Prefeito mais votado em São Paulo
select*
from resultado2020
where NM_MUNICIPIO in ('SÃO PAULO') AND DS_CARGO_PERGUNTA in ('Prefeito')
Order BY QT_VOTOS DESC;
-- Vereador mais votado em São Paulo
select*
from resultado2020
where NM_MUNICIPIO in ('SÃO PAULO') AND DS_CARGO_PERGUNTA in ('Vereador')
Order BY QT_VOTOS DESC;
-- Maior numero de votos
select MAX(QT_VOTOS)
from resultado2020
-- O
select NM_VOTAVEL AS CANDIDATO,
COUNT (QT_VOTOS) AS TOTAL_VOTOS
FROM resultado2020
GROUP BY NM_VOTAVEL;
DELETE
FROM resultado2020
WHERE DS_TIPO_VOTAVEL = 'Legenda';
DELETE
FROM resultado2020
WHERE DS_TIPO_VOTAVEL = 'Nulo';
DELETE
FROM resultado2020
WHERE DS_TIPO_VOTAVEL = 'Branco';
DELETE
FROM perfil_eleitorado_2020
WHERE DS_GENERO = 'NÃO INFORMADO';
DELETE
FROM perfil_eleitorado_2020
WHERE SG_UF='”AC”';
EXEC sp_help 'perfil_eleitorado_2020'
EXEC sp_rename 'perfil_eleitorado."SG_UF"','SIGLA_UF','Column_name';
select *
FROM perfil_eleitorado;
EXEC sp_help 'perfil_eleitorado_2020'
select* from resultado2020
inner join perfil_eleitorado_2020
on perfil_eleitorado_2020.CD_MUNICIPIO = resultado2020.CD_MUNICIPIO
select CD_MUNICIPIO,NM_MUNICIPIO,DS_GENERO
from perfil_eleitorado_2020
group by CD_MUNICIPIO ;
select NM_VOTAVEL, COUNT (NM_MUNICIPIO)
from resultado2020
left join perfil_eleitorado_2020
on resultado2020.NM_MUNICIPIO=perfil_eleitorado_2020.NM_MUNICIPIO
GROUP BY NM_VOTAVEL, NM_MUNICIPIO;
select* from resultado2020
inner join perfil_eleitorado_2020
on perfil_eleitorado_2020.CD_MUNICIPIO = resultado2020.CD_MUNICIPIO
select COUNT (DS_GENERO) AS QTD_FEMININO , NM_MUNICIPIO
from perfil_eleitorado_2020
WHERE DS_GENERO = '"FEMININO"'
GROUP BY NM_MUNICIPIO;
select COUNT (DS_GENERO) AS QTD_FEMININO , NM_MUNICIPIO
from perfil_eleitorado_2020
WHERE DS_GENERO = '"MASCULINO"'
GROUP BY NM_MUNICIPIO;
DELETE
FROM perfil_eleitorado_2020
WHERE DS_FAIXA_ETARIA = '"Inválido"';
DELETE
FROM perfil_eleitorado_2020
WHERE SG_UF ='"RJ"';
UPDATE perfil_eleitorado_2020
SET DS_GENERO = 'NE'
WHERE DS_GENERO = '["NÃO INFORMADO"]'
alter table perfil_eleitorado_2020
drop column DT_GERACAO, HH_GERACAO
alter table perfil_eleitorado
drop column "QT_ELEITORES_BIOMETRIA"
