O armazenamento é limitado pelo espaço em disco ou por um limite restritivo no *número máximo* de índices ou documentos, o que chegar primeiro.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrato de Nível de Serviço (SLA) |N.º <sup>1</sup> |Sim |Sim |Sim |Sim |Sim |
| Armazenamento por partição |50 MB |2GB |25 GB |100 GB |200 GB |200 GB |
| Partições por serviço |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Tamanho da partição |N/D |2GB |25 GB |100 GB |200 GB |200 GB |
| Réplicas |N/D |3 |12 |12 |12 |12 |
| Índices máximos |3 |5 |50 |200 |200 |1000 por partição ou 3000 por serviço |
| Indexadores máximos |3 |5 |50 |200 |200 |Sem suporte de indexador |
| Origens de dados máximas |3 |5 |50 |200 |200 |Sem suporte de indexador |
| Documentos máximos |10,000 |1 milhão |15 milhões por partição ou 180 milhões por serviço |60 milhões por partição ou 720 milhões por serviço |120 milhões por partição ou 1,4 biliões por serviço |1 milhão por índice ou 200 milhões por partição |
| Consultas estimadas por segundo (QPS) |N/D |~3 por réplica |~15 por réplica |~60 por réplica |~60 por réplica |>60 por réplica |

<sup>1</sup> Os SKUs gratuitos e de Pré-visualização não dispõem de contratos de nível de serviço (SLAs). Os SLAs são impostos assim que um SKU se tornar geralmente disponível.

<sup>2</sup> O S3 HD tem um limite restritivo de 3 partições, que é inferior ao limite de partição do S3. O limite de partição inferior é imposto porque a contagem de índice do S3 HD é significativamente mais elevada. Dado que existem limites de serviço para recursos informáticos (processamento e armazenamento) e conteúdo (índices e documentos), o limite de conteúdo é atingido primeiro.


<!--HONumber=Feb17_HO2-->


