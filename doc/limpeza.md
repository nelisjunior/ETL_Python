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
df.loc[1,'ocorrencia_cidade']
```




    'GUARULHOS'




```python
df.loc[[10,40]]
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
      <th>40</th>
      <td>45415</td>
      <td>45415</td>
      <td>45415</td>
      <td>45415</td>
      <td>45415</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>RIO DE JANEIRO</td>
      <td>RJ</td>
      <td>...</td>
      <td>2012-01-30</td>
      <td>13:55:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-077/CENIPA/2013</td>
      <td>SIM</td>
      <td>21/10/2013</td>
      <td>0</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 22 columns</p>
</div>




```python
df.loc[:,'ocorrencia_cidade']
```




    0        PORTO ALEGRE
    1           GUARULHOS
    2              VIAMÃO
    3       SÃO SEBASTIÃO
    4            SÃO SEPÉ
                ...      
    5162            JATAÍ
    5163          MARACAÍ
    5164    NOVO HAMBURGO
    5165         CURITIBA
    5166        PETROLINA
    Name: ocorrencia_cidade, Length: 5167, dtype: object




```python
df.codigo_ocorrencia.is_unique
```




    True




```python
df.set_index('codigo_ocorrencia', inplace=True)
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
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
    <tr>
      <th>codigo_ocorrencia</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>52242</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
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
      <th>45331</th>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>45331</td>
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>BRASIL</td>
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
      <th>45333</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>BRASIL</td>
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
      <th>45401</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>BRASIL</td>
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
      <th>45407</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>BRASIL</td>
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
<p>5 rows × 21 columns</p>
</div>




```python
df.loc[45407]
```




    codigo_ocorrencia1                              45407
    codigo_ocorrencia2                              45407
    codigo_ocorrencia3                              45407
    codigo_ocorrencia4                              45407
    ocorrencia_classificacao                     ACIDENTE
    ocorrencia_latitude                               ***
    ocorrencia_longitude                              ***
    ocorrencia_cidade                            SÃO SEPÉ
    ocorrencia_uf                                      RS
    ocorrencia_pais                                BRASIL
    ocorrencia_aerodromo                             ****
    ocorrencia_dia                    2012-01-06 00:00:00
    ocorrencia_hora                              16:30:00
    investigacao_aeronave_liberada                    SIM
    investigacao_status                        FINALIZADA
    divulgacao_relatorio_numero         A-071/CENIPA/2013
    divulgacao_relatorio_publicado                    SIM
    divulgacao_dia_publicacao                  27/11/2013
    total_recomendacoes                                 0
    total_aeronaves_envolvidas                          1
    ocorrencia_saida_pista                            NÃO
    Name: 45407, dtype: object




```python
df.reset_index(drop=True, inplace=True )
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
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
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
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
      <td>ACIDENTE</td>
      <td>-234.355.555.556</td>
      <td>-464.730.555.556</td>
      <td>GUARULHOS</td>
      <td>SP</td>
      <td>BRASIL</td>
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
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>BRASIL</td>
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
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>BRASIL</td>
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
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>BRASIL</td>
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
<p>5 rows × 21 columns</p>
</div>




```python
df.loc[0,'ocorrencia_aerodromo'] = ''
```


```python
df.head(1)
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
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
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
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
  </tbody>
</table>
<p>1 rows × 21 columns</p>
</div>




```python
df.loc[1]=20
```


```python
df.head(2)
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
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
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2012-01-05 00:00:00</td>
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
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>...</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 21 columns</p>
</div>




```python
df.loc[:,'total_recomendacoes'] = 10
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
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
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2012-01-05 00:00:00</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>...</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>10</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2012-01-06 00:00:00</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2012-01-06 00:00:00</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2012-01-06 00:00:00</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>10</td>
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
      <td>ACIDENTE</td>
      <td>-17.999.194</td>
      <td>-51.642.861</td>
      <td>JATAÍ</td>
      <td>GO</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2021-12-30 00:00:00</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>ACIDENTE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2021-12-31 00:00:00</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5164</th>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>80457</td>
      <td>INCIDENTE GRAVE</td>
      <td>-29.695.833</td>
      <td>-51.081.667</td>
      <td>NOVO HAMBURGO</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2021-12-31 00:00:00</td>
      <td>11:59:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5165</th>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>80460</td>
      <td>INCIDENTE</td>
      <td>-25.403.333</td>
      <td>-49.233.611</td>
      <td>CURITIBA</td>
      <td>PR</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2021-12-31 00:00:00</td>
      <td>15:12:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
    <tr>
      <th>5166</th>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>80467</td>
      <td>INCIDENTE</td>
      <td>-93.675</td>
      <td>-4.056.361.111.111</td>
      <td>PETROLINA</td>
      <td>PE</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>2021-12-31 00:00:00</td>
      <td>20:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
    </tr>
  </tbody>
</table>
<p>5167 rows × 21 columns</p>
</div>




```python
df['ocorrencia_uf_bkp'] = df.ocorrencia_uf
```


```python
df.loc[df.ocorrencia_uf == 'SP', ['ocorrencia_classificacao']] = 'GRAVE'
```


```python
df.loc[df.ocorrencia_uf == 'SP']
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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
      <th>...</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
      <th>ocorrencia_uf_bkp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>GRAVE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>5</th>
      <td>52243</td>
      <td>52243</td>
      <td>52243</td>
      <td>52243</td>
      <td>GRAVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>UBATUBA</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>14:30:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>6</th>
      <td>50713</td>
      <td>50713</td>
      <td>50713</td>
      <td>50713</td>
      <td>GRAVE</td>
      <td>***</td>
      <td>***</td>
      <td>CAMPINAS</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>18:15:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>IG-184/CENIPA/2013</td>
      <td>SIM</td>
      <td>08/01/2014</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>13</th>
      <td>45408</td>
      <td>45408</td>
      <td>45408</td>
      <td>45408</td>
      <td>GRAVE</td>
      <td>-245.888.888.889</td>
      <td>-482.113.888.889</td>
      <td>ELDORADO</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>13:45:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-509/CENIPA/2021</td>
      <td>SIM</td>
      <td>08/07/2021</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>26</th>
      <td>45410</td>
      <td>45410</td>
      <td>45410</td>
      <td>45410</td>
      <td>GRAVE</td>
      <td>-23.005.278</td>
      <td>-46.636.944</td>
      <td>BRAGANÇA PAULISTA</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>23:30:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>SIM</td>
      <td>SP</td>
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
      <th>5148</th>
      <td>80441</td>
      <td>80441</td>
      <td>80441</td>
      <td>80441</td>
      <td>GRAVE</td>
      <td>-230.052</td>
      <td>-466.336</td>
      <td>BRAGANÇA PAULISTA</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>18:15:00</td>
      <td>NÃO</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>SIM</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>5157</th>
      <td>80453</td>
      <td>80453</td>
      <td>80453</td>
      <td>80453</td>
      <td>GRAVE</td>
      <td>-2.300.694.444.444</td>
      <td>-4.713.444.444.444</td>
      <td>CAMPINAS</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>09:00:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>5158</th>
      <td>80454</td>
      <td>80454</td>
      <td>80454</td>
      <td>80454</td>
      <td>GRAVE</td>
      <td>-21.144.167</td>
      <td>-50.426.389</td>
      <td>ARAÇATUBA</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>21:35:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>SIM</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>5161</th>
      <td>80456</td>
      <td>80456</td>
      <td>80456</td>
      <td>80456</td>
      <td>GRAVE</td>
      <td>-23.626.111</td>
      <td>-46.656.389</td>
      <td>SÃO PAULO</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>13:15:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>SIM</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>5163</th>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>80452</td>
      <td>GRAVE</td>
      <td>-22.585.556</td>
      <td>-50.753.889</td>
      <td>MARACAÍ</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>09:30:00</td>
      <td>SIM</td>
      <td>ATIVA</td>
      <td>A DEFINIR</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
<p>1260 rows × 22 columns</p>
</div>


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
      <th>codigo_ocorrencia1</th>
      <th>codigo_ocorrencia2</th>
      <th>codigo_ocorrencia3</th>
      <th>codigo_ocorrencia4</th>
      <th>ocorrencia_classificacao</th>
      <th>ocorrencia_latitude</th>
      <th>ocorrencia_longitude</th>
      <th>ocorrencia_cidade</th>
      <th>ocorrencia_uf</th>
      <th>ocorrencia_pais</th>
      <th>...</th>
      <th>ocorrencia_hora</th>
      <th>investigacao_aeronave_liberada</th>
      <th>investigacao_status</th>
      <th>divulgacao_relatorio_numero</th>
      <th>divulgacao_relatorio_publicado</th>
      <th>divulgacao_dia_publicacao</th>
      <th>total_recomendacoes</th>
      <th>total_aeronaves_envolvidas</th>
      <th>ocorrencia_saida_pista</th>
      <th>ocorrencia_uf_bkp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>52242</td>
      <td>INCIDENTE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PORTO ALEGRE</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>20:27:00</td>
      <td>***</td>
      <td>FINALIZADA</td>
      <td>***</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>RS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>...</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>10</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>45333</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>VIAMÃO</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>13:00:00</td>
      <td>NaN</td>
      <td>FINALIZADA</td>
      <td>A-070/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>RS</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>45401</td>
      <td>GRAVE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEBASTIÃO</td>
      <td>SP</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>17:00:00</td>
      <td>***</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NÃO</td>
      <td>NaN</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>45407</td>
      <td>ACIDENTE</td>
      <td>***</td>
      <td>***</td>
      <td>SÃO SEPÉ</td>
      <td>RS</td>
      <td>BRASIL</td>
      <td>...</td>
      <td>16:30:00</td>
      <td>SIM</td>
      <td>FINALIZADA</td>
      <td>A-071/CENIPA/2013</td>
      <td>SIM</td>
      <td>27/11/2013</td>
      <td>10</td>
      <td>1</td>
      <td>NÃO</td>
      <td>RS</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
df.loc[df.ocorrencia_aerodromo == '****', ['ocorrencia_aerodromo']] = pd.NA
```


```python

```
