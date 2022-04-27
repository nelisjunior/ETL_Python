```python
import pandas as pd
import pandera as pa
```


```python
df = pd.read_csv("ocorrencia.csv", sep=";", parse_dates=['ocorrencia_dia'], dayfirst=True, encoding='latin-1')
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5162</th>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>...</td>
      <td>2021-12-30</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 22 columns</p>
</div>




```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
df.loc[df.ocorrencia_aerodromo == '###!', ['ocorrencia_aerodromo']] = pd.NA
```


```python
df.loc[1:20,'ocorrencia_aerodromo']
```




    1     SBGR
    2     <NA>
    3     <NA>
    4     <NA>
    5     <NA>
    6     SDAI
    7     SBBE
    8     <NA>
    9     SBUL
    10    <NA>
    11    SBPA
    12    SBMA
    13    <NA>
    14    <NA>
    15    <NA>
    16    <NA>
    17    SBBR
    18    SNWC
    19    <NA>
    20    SBPR
    Name: ocorrencia_aerodromo, dtype: object


ocorrencia_latitude
\t
***
****
*********
ocorrencia_longitude
\t
***
****
*********
ocorrencia_uf
**
ocorrencia_aerodromo
###!
####
****
*****
ocorrencia_hora
NULL
investigacao_aeronave_liberada
NULL
***
divulgacao_relatorio_numero
***
NULL
divulgacao_dia_publicacao
NULL

```python
df.replace(['\t','***','****','*****','###!','####','NaN','NULL'], pd.NA, inplace=True)
```


```python
df.isna().sum()
```




    codigo_ocorrencia                    0
    codigo_ocorrencia1                   0
    codigo_ocorrencia2                   0
    codigo_ocorrencia3                   0
    codigo_ocorrencia4                   0
    ocorrencia_classificacao             0
    ocorrencia_latitude               1493
    ocorrencia_longitude              1494
    ocorrencia_cidade                    0
    ocorrencia_uf                        0
    ocorrencia_pais                      0
    ocorrencia_aerodromo              1905
    ocorrencia_dia                       0
    ocorrencia_hora                      1
    investigacao_aeronave_liberada    1778
    investigacao_status                257
    divulgacao_relatorio_numero       3291
    divulgacao_relatorio_publicado       0
    divulgacao_dia_publicacao         3816
    total_recomendacoes                  0
    total_aeronaves_envolvidas           0
    ocorrencia_saida_pista               0
    dtype: int64




```python
df.fillna(10, inplace=True)
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>&lt;NA&gt;</td>
      <td>FINALIZADA</td>
      <td>&lt;NA&gt;</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>&lt;NA&gt;</td>
      <td>&lt;NA&gt;</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>&lt;NA&gt;</td>
      <td>&lt;NA&gt;</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>&lt;NA&gt;</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>&lt;NA&gt;</td>
      <td>&lt;NA&gt;</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5162</th>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>...</td>
      <td>2021-12-30</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>&lt;NA&gt;</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>&lt;NA&gt;</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>&lt;NA&gt;</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 22 columns</p>
</div>




```python
df.replace([10], pd.NA, inplace=True)
```


```python
df.fillna(value={'total_recomendacoes':10}, inplace=True)
```


```python
df['total_recomendacoes_bkp'] = df.total_recomendacoes
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
df.drop(['total_recomendacoes_bkp'], axis=1, inplace=True)
```


```python
df.dropna()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>6</th>
      <td>50713</td>
      <td>50713</td>
      <td>50713</td>
      <td>50713</td>
      <td>50713</td>
      <td>INCIDENTE GRAVE</td>
      <td>***</td>
      <td>***</td>
      <td>CAMPINAS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-07</td>
      <td>18:15:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>IG-184/CENIPA/2013</td>
      <td>SIM</td>
      <td>08/01/2014</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>10</th>
      <td>45332</td>
      <td>45332</td>
      <td>45332</td>
      <td>45332</td>
      <td>45332</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-09</td>
      <td>13:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-072/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>12</th>
      <td>45396</td>
      <td>45396</td>
      <td>45396</td>
      <td>45396</td>
      <td>45396</td>
      <td>INCIDENTE GRAVE</td>
      <td>-53.677.777.778</td>
      <td>-491.383.333.333</td>
      <td>MARABÁ</td>
      <td>PA</td>
      <td>...</td>
      <td>2012-01-11</td>
      <td>11:21:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>IG-508/CENIPA/2017</td>
      <td>SIM</td>
      <td>02/05/2017</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4549</th>
      <td>79671</td>
      <td>79671</td>
      <td>79671</td>
      <td>79671</td>
      <td>79671</td>
      <td>ACIDENTE</td>
      <td>\t-25.490278\t</td>
      <td>\t-54.280278\t</td>
      <td>SÃO MIGUEL DO IGUAÇU</td>
      <td>PR</td>
      <td>...</td>
      <td>2020-11-14</td>
      <td>12:40:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-139/CENIPA/2020</td>
      <td>SIM</td>
      <td>08/07/2021</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4570</th>
      <td>79692</td>
      <td>79692</td>
      <td>79692</td>
      <td>79692</td>
      <td>79692</td>
      <td>ACIDENTE</td>
      <td>-21.148.611</td>
      <td>-48.988.056</td>
      <td>CATANDUVA</td>
      <td>SP</td>
      <td>...</td>
      <td>2020-11-28</td>
      <td>12:50:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-140/CENIPA/2020</td>
      <td>SIM</td>
      <td>21/07/2021</td>
      <td>1</td>
      <td>1</td>
      <td>SIM</td>
    </tr>
    <tr>
      <th>4582</th>
      <td>79713</td>
      <td>79713</td>
      <td>79713</td>
      <td>79713</td>
      <td>79713</td>
      <td>ACIDENTE</td>
      <td>\t-33.176944\t</td>
      <td>\t-53.014167\t</td>
      <td>SANTA VITÓRIA DO PALMAR</td>
      <td>RS</td>
      <td>...</td>
      <td>2020-12-06</td>
      <td>13:15:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-146/CENIPA/2020</td>
      <td>SIM</td>
      <td>08/07/2021</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4595</th>
      <td>79729</td>
      <td>79729</td>
      <td>79729</td>
      <td>79729</td>
      <td>79729</td>
      <td>ACIDENTE</td>
      <td>-2.803.889</td>
      <td>-48.935.833</td>
      <td>TAILÂNDIA</td>
      <td>PA</td>
      <td>...</td>
      <td>2020-12-15</td>
      <td>20:00:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-152/CENIPA/2020</td>
      <td>SIM</td>
      <td>30/12/2021</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4833</th>
      <td>80073</td>
      <td>80073</td>
      <td>80073</td>
      <td>80073</td>
      <td>80073</td>
      <td>ACIDENTE</td>
      <td>-1.098.472</td>
      <td>-3.705.166</td>
      <td>ARACAJU</td>
      <td>SE</td>
      <td>...</td>
      <td>2021-05-06</td>
      <td>14:57:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-063/CENIPA/2021</td>
      <td>SIM</td>
      <td>12/11/2021</td>
      <td>2</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>1256 rows × 22 columns</p>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5162</th>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>...</td>
      <td>2021-12-30</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 22 columns</p>
</div>




```python
df.dropna(subset=['ocorrencia_uf'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5162</th>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>...</td>
      <td>2021-12-30</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 22 columns</p>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>codigo_ocorrencia</th>
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>...</th>
      <th>ocorrencia_dia</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-05</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:44:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-582/CENIPA/2014</td>
      <td>SIM</td>
      <td>01/09/2016</td>
      <td>3</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>...</td>
      <td>2012-01-06</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5162</th>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>80458</td>
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>...</td>
      <td>2021-12-30</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>...</td>
      <td>2021-12-31</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 22 columns</p>
</div>




```python
df.drop_duplicates(inplace=True)
```
